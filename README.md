function time_response(sys_long, sys_lat, params)

% TIME_RESPONSE  Step & impulse responses of open‑loop transfer functions.

    s = tf('s');
    
    A_aug = [sys_long.A, zeros(4,1); 0,-1,0,params.U0,0];
    B_aug = [sys_long.B; 0];
    C_aug = [sys_long.C, zeros(4,1); zeros(1,4),1];
    sys_aug = ss(A_aug,B_aug,C_aug,0);
    
    sys_h_de = tf(sys_aug(5,1));
    sys_psi_da = tf(sys_lat(5,1));
    
    figure('Name','Step & Impulse Responses');
    subplot(221); step(sys_h_de); grid on;
    title('Step: Elevator → Altitude');
    
    subplot(222); step(sys_psi_da); grid on;
    title('Step: Aileron → Heading');
    
    subplot(223); impulse(sys_h_de); grid on;
    title('Impulse: Elevator → Altitude');
    subplot(224); impulse(sys_psi_da); grid on;
    title('Impulse: Aileron → Heading');
    
end
