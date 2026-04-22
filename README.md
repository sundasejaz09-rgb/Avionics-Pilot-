function [t, h, elev] = simulate_altitude(sys_long, params)

% SIMULATE_ALTITUDE  Closed‑loop altitude hold with PI controller.

    s = tf('s');
    
    A_aug = [sys_long.A, zeros(4,1); 0,-1,0,params.U0,0];
    B_aug = [sys_long.B; 0];
    C_aug = [sys_long.C, zeros(4,1); zeros(1,4),1];
    sys_aug = ss(A_aug,B_aug,C_aug,0);
    sys_h_de = tf(sys_aug(5,1));
    C_alt = 0.025 + 0.0015/s;
    act_elev = 1/(0.1*s+1);
    cl = feedback(C_alt * act_elev * sys_h_de, 1);
    t = (0:0.05:60)';
    cmd = 152.4 * ones(size(t));
    h = lsim(cl, cmd, t);
    elev = lsim(C_alt, cmd - h, t);
    
end
