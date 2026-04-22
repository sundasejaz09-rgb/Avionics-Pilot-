function performance_metrics(t, y, cmd, name)

% PERFORMANCE_METRICS  Compute and display step response characteristics.

    info = stepinfo(y, t, cmd, 'SettlingTimeThreshold',0.02);
    fprintf('\n=== %s ===\n', name);
    fprintf('  Rise Time: %.2f s\n', info.RiseTime);
    fprintf('  Settling Time: %.2f s\n', info.SettlingTime);
    fprintf('  Overshoot: %.1f %%\n', info.Overshoot);
    fprintf('  Steady‑state error: %.3f\n', abs(y(end)-cmd));
    
end
