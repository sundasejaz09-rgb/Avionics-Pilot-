% AeroPilot – Cessna 172 Flight Controller Main Script
clear; close all; clc;
addpath(genpath('models'), genpath('controllers'), genpath('analysis'), genpath('simulation'));

params = aircraft_params();
sys_long = longitudinal_model(params);
sys_lat  = lateral_model(params);

stability_analysis(sys_long, sys_lat);
controllability_analysis(sys_long, sys_lat);
frequency_response(sys_long, sys_lat, params);
time_response(sys_long, sys_lat, params);

[t_alt, h, elev] = simulate_altitude(sys_long, params);
[t_psi, psi, ail] = simulate_heading(sys_lat, params);

performance_metrics(t_alt, h, 152.4, 'Altitude (500 ft)');
performance_metrics(t_psi, psi, 90*pi/180, 'Heading (90°)');

plot_results(t_alt, h, elev, t_psi, psi, ail);
disp('Simulation complete.');
