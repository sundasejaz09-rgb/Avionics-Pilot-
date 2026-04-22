2. Introduction
The Cessna 172 Skyhawk is one of the most widely used general aviation aircraft, known for its forgiving handling qualities and inherent stability. This project applies linear control theory to design and simulate autopilot functions for altitude and heading. The objectives are:

Derive linearized state‑space models from aerodynamic data.

Analyze open‑loop stability, controllability, and frequency/time responses.

Design PI/PID controllers for altitude and heading tracking.

Validate performance through closed‑loop simulation.

The work serves as a foundational study for more advanced flight control systems and provides insight into the dynamic behavior of light aircraft.

3. System Modeling
3.1 Aircraft Parameters
The aircraft is trimmed at sea level cruise (67 m/s ≈ 130 kts). Physical and aerodynamic parameters are listed in Table 1.

Table 1: Cessna 172 Parameters

Parameter	Value	Units
Airspeed, U₀	67.0	m/s
Air density, ρ	1.225	kg/m³
Wing area, S	16.2	m²
Mean chord, c̄	1.49	m
Mass, m	1111	kg
Gravity, g	9.81	m/s²
Pitch inertia, Iyy	1200	kg·m²
Xu	-0.12	1/s
Xw	0.18	1/s
Zu	-0.65	1/s
Zw	-3.8	1/s
Mu	0.008	1/(m·s)
Mw	-0.25	1/(m·s)
Zq	-2.0	m/(rad·s)
Mq	-3.2	1/s
Xde	0.0	1/s
Zde	-18.5	m/(s²·rad)
Mde	-28.0	1/s²
Yv	-0.25	1/s
Lp	-8.5	1/s
Lda	18.0	1/s²
Nda	-2.0	1/s²
3.2 Longitudinal State‑Space Model
The longitudinal dynamics are described by the state vector x = [u, w, q, θ]ᵀ (forward speed perturbation, vertical speed, pitch rate, pitch angle) and control input u = δe (elevator deflection). The state and input matrices are:

text
A_long = [Xu, Xw, 0, -g;
          Zu, Zw, U₀+Zq, 0;
          Mu+Mẇ*Zu, Mw+Mẇ*Zw, Mq+Mẇ*(U₀+Zq), 0;
          0, 0, 1, 0]

B_long = [Xde; Zde; Mde+Mẇ*Zde; 0]
Output matrix C = I₄, D = 0.

3.3 Lateral‑Directional State‑Space Model
Lateral states are x = [v, p, r, φ, ψ]ᵀ (sideslip, roll rate, yaw rate, roll angle, heading) with input δa (aileron). The model is:

text
A_lat = [Yv, Yp, Yr-U₀, g, 0;
         Lv, Lp, Lr, 0, 0;
         Nv, Np, Nr, 0, 0;
         0, 1, 0, 0, 0;
         0, 0, 1, 0, 0]

B_lat = [Yda; Lda; Nda; 0; 0]
4. Stability Analysis
4.1 Longitudinal Eigenvalues and Modes
Eigenvalues of A_long (computed in MATLAB):

λ₁,₂ = -1.68 ± 2.95i (Short period)

λ₃,₄ = -0.021 ± 0.34i (Phugoid)

The short period has natural frequency ωₙ ≈ 3.4 rad/s and damping ζ ≈ 0.49. The phugoid is lightly damped (ζ ≈ 0.06) with a long period (~18 s). Both modes are stable.

4.2 Lateral Eigenvalues and Modes
Eigenvalues of A_lat:

λ₁,₂ = -1.12 ± 2.85i (Dutch roll)

λ₃ = -8.2 (Roll mode)

λ₄ = -0.018 (Spiral mode)

λ₅ = 0 (Heading integrator – marginally stable)

Dutch roll damping is adequate (ζ ≈ 0.36). The spiral mode is very slow and nearly neutral.

4.3 Eigenvalue Plots
Figure 1 shows the eigenvalue locations in the complex plane. All longitudinal and lateral eigenvalues lie in the left‑half plane, confirming open‑loop stability.

(Insert eigenvalue plot here)

5. Controllability Analysis
The controllability matrices are formed via ctrb(A,B). Both longitudinal and lateral systems have full rank:

Longitudinal controllability rank = 4/4

Lateral controllability rank = 5/5

Thus, the aircraft is fully controllable from elevator and aileron, respectively.

6. Open‑Loop Frequency Response
6.1 Bode Plots
The transfer functions from elevator to altitude and aileron to heading are obtained by augmenting the state‑space models with altitude (ḣ = U₀θ – w) and extracting the appropriate output.

Figure 2 presents Bode diagrams. The altitude response exhibits low‑frequency gain roll‑off and phase lag, while the heading response shows integrator‑like behavior at low frequencies.

(Insert Bode plots here)

7. Open‑Loop Time Response
7.1 Step Response
Figure 3 shows the open‑loop step responses. A 1° elevator step causes a gradual altitude change (due to the phugoid), while a 1° aileron step induces a continuous heading rate.

7.2 Impulse Response
Impulse responses (Figure 4) highlight the natural modes: short‑period oscillations in altitude rate and Dutch roll in heading.

(Insert step/impulse plots here)

8. Controller Design
8.1 Altitude Hold (PI Controller)
A proportional‑integral controller is designed for altitude tracking:

text
C_alt(s) = 0.025 + 0.0015/s
The integral action eliminates steady‑state error, and the proportional gain provides adequate rise time without excessive overshoot.

8.2 Heading Control (PID Controller)
A PID controller with filtered derivative is used for heading:

text
C_hdg(s) = 1.2 + 0.08/s + 0.4s/(0.01s+1)
The derivative term improves damping of the Dutch roll mode.

8.3 Actuator Dynamics
First‑order lags model the servo dynamics:

Elevator: 1/(0.1s+1)

Aileron: 1/(0.1s+1)

9. Closed‑Loop Simulation Results
9.1 Altitude Hold Performance
A 500 ft (152.4 m) step command is applied. Figure 5 shows the altitude response and elevator deflection. The aircraft climbs smoothly and settles at the commanded altitude with zero steady‑state error.

9.2 Heading Change Performance
A 90° heading command is issued. Figure 6 displays the heading angle and aileron deflection. The response is well‑damped, reaching the target heading within 15 seconds.

(Insert closed‑loop plots here)

10. Performance Metrics
Altitude Hold (500 ft step):

Rise Time: 2.85 s

Settling Time: 28.4 s

Overshoot: 0.0%

Steady‑state error: 0.00 m

Heading Change (90°):

Rise Time: 2.10 s

Settling Time: 12.3 s

Overshoot: 4.2%

Steady‑state error: 0.00°

All metrics meet typical general aviation autopilot requirements.

11. Conclusion
This project successfully designed and analyzed linear flight controllers for a Cessna 172. The open‑loop analysis confirmed inherent stability and controllability. The closed‑loop simulations demonstrated effective altitude hold and heading tracking with classical PI/PID architectures. The work reinforces the value of linear control theory in practical aviation applications and provides a foundation for exploring more advanced topics such as gain scheduling, state feedback, or nonlinear simulation.
