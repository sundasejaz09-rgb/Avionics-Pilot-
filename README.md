function stability_analysis(sys_long, sys_lat)

% STABILITY_ANALYSIS  Eigenvalues, damping, and eigenvalue plots.

    fprintf('=== STABILITY ANALYSIS ===\n');
    e_long = eig(sys_long.A);
    fprintf('Longitudinal eigenvalues:\n'); disp(e_long);
    [wn,z] = damp(sys_long.A);
    fprintf('Mode   wn (rad/s)  damping\n');
    for i=1:length(wn)
        fprintf('%d      %.4f      %.4f\n',i,wn(i),z(i));
        
    end
    
    e_lat = eig(sys_lat.A);
    fprintf('\nLateral eigenvalues:\n'); disp(e_lat);
    [wn,z] = damp(sys_lat.A);
    for i=1:length(wn)
        fprintf('%d      %.4f      %.4f\n',i,wn(i),z(i));
        
    end
    
    figure('Name','Eigenvalue Analysis');
    
    subplot(121);
    plot(real(e_long), imag(e_long), 'rx', 'MarkerSize',10,'LineWidth',2); hold on;
    xline(0,'k--'); yline(0,'k--');
    xlabel('Real'); ylabel('Imag'); title('Longitudinal Eigenvalues');
    grid on; axis equal;
    
    subplot(122);
    plot(real(e_lat), imag(e_lat), 'bx', 'MarkerSize',10,'LineWidth',2); hold on;
    xline(0,'k--'); yline(0,'k--');
    xlabel('Real'); ylabel('Imag'); title('Lateral Eigenvalues');
    grid on; axis equal;
    
end
