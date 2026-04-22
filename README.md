function frequency_response(sys_long, sys_lat, params)

% FREQUENCY_RESPONSE  Bode plots for elevator→altitude and aileron→heading.

    s = tf('s');
    
    A_aug = [sys_long.A, zeros(4,1); 0,-1,0,params.U0,0];
    B_aug = [sys_long.B; 0];
    C_aug = [sys_long.C, zeros(4,1); zeros(1,4),1];
    sys_aug = ss(A_aug,B_aug,C_aug,0);
    sys_h_de = tf(sys_aug(5,1));
    sys_psi_da = tf(sys_lat(5,1));
    
    figure('Name','Bode Plots');
    subplot(211); bode(sys_h_de); grid on;
    title('Elevator → Altitude');
    
    subplot(212); bode(sys_psi_da); grid on;
    title('Aileron → Heading');
end
