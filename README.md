function [t, psi, ail] = simulate_heading(sys_lat, params)

% SIMULATE_HEADING  Closed‑loop heading change with PID controller.

    s = tf('s');
    sys_psi_da = tf(sys_lat(5,1));
    Kp=1.2; Ki=0.08; Kd=0.4; N=100;
    C_hdg = Kp + Ki/s + Kd*s/(N*s+1);
    act_ail = 1/(0.1*s+1);
    cl = feedback(C_hdg * act_ail * sys_psi_da, 1);
    t = (0:0.05:40)';
    cmd = (90*pi/180) * ones(size(t));
    psi = lsim(cl, cmd, t);
    ail = lsim(C_hdg, cmd - psi, t);
end
