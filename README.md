function params = aircraft_params()

% AIRCRAFT_PARAMS  Cessna 172 parameters (sea level, cruise)

    params.U0   = 67.0;           % m/s (~130 kts)
    params.rho  = 1.225;          % kg/m³
    params.S    = 16.2;           % m²
    params.cbar = 1.49;           % m
    params.mass = 1111;           % kg
    params.g    = 9.81;           % m/s²
    params.Ixx  = 1200;           % kg·m²
    params.Iyy  = 1200;
    params.Izz  = 2000;
    params.Ixz  = 0;

    % Longitudinal dimensional derivatives
    
    params.Xu = -0.12;    params.Xw = 0.18;
    params.Zu = -0.65;    params.Zw = -3.8;
    params.Mu = 0.008;    params.Mw = -0.25;
    params.Zq = -2.0;     params.Mq = -3.2;
    params.Mwd = 0.0;

    % Control derivatives (elevator)
    
    params.Xde = 0.0;     params.Zde = -18.5;
    params.Mde = -28.0;

    % Lateral derivatives
    
    params.Yv = -0.25;    params.Yp = 0.0;      params.Yr = 0.0;
    params.Lv = -0.12;    params.Lp = -8.5;     params.Lr = 2.5;
    params.Nv = 0.05;     params.Np = -0.8;     params.Nr = -1.2;
    params.Yda = 0.0;     params.Ydr = 2.5;
    params.Lda = 18.0;    params.Ldr = 5.0;
    params.Nda = -2.0;    params.Ndr = -8.0;
end
