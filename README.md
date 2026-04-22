function C = heading_controller()

% HEADING_CONTROLLER  PID controller (filtered derivative) for heading.

    s = tf('s');
    
    Kp = 1.2;   Ki = 0.08;   Kd = 0.4;   N = 100;
    
    C = Kp + Ki/s + Kd*s/(N*s+1);
    
end
