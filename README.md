function plot_results(t_alt, h, elev, t_psi, psi, ail)

% PLOT_RESULTS  Closed‑loop simulation plots.

    figure('Name','Altitude Control');
    subplot(211); plot(t_alt, h); hold on; yline(152.4,'r--');
    xlabel('Time (s)'); ylabel('Altitude (m)'); grid on;
    legend('Actual','Command'); title('Cessna 172 Altitude Hold (500 ft)');
    subplot(212); plot(t_alt, rad2deg(elev)); xlabel('Time (s)');
    ylabel('Elevator (deg)'); grid on;

    figure('Name','Heading Control');
    subplot(211); plot(t_psi, rad2deg(psi)); hold on; yline(90,'r--');
    xlabel('Time (s)'); ylabel('Heading (deg)'); grid on;
    legend('Actual','Command'); title('Cessna 172 Heading Change (90°)');
    subplot(212); plot(t_psi, rad2deg(ail)); xlabel('Time (s)');
    ylabel('Aileron (deg)'); grid on;
    
end
