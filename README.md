function C = altitude_controller()

% ALTITUDE_CONTROLLER  PI controller for altitude hold.

    s = tf('s');
    Kp = 0.025;
    Ki = 0.0015;
    C = Kp + Ki/s;
    
end
