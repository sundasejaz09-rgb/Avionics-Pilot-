function [act_elev, act_ail] = actuator_models()

% ACTUATOR_MODELS  First‑order actuator transfer functions.

    s = tf('s');
    act_elev = 1/(0.1*s+1);
    act_ail  = 1/(0.1*s+1);
    
end
