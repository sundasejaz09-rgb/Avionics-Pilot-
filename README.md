function controllability_analysis(sys_long, sys_lat)

% CONTROLLABILITY_ANALYSIS  Check controllability ranks.

    fprintf('\n=== CONTROLLABILITY ===\n');
    CoL = ctrb(sys_long.A, sys_long.B);
    fprintf('Longitudinal rank: %d/%d\n', rank(CoL), size(sys_long.A,1));
    CoLat = ctrb(sys_lat.A, sys_lat.B);
    fprintf('Lateral rank:      %d/%d\n', rank(CoLat), size(sys_lat.A,1));
    
end
