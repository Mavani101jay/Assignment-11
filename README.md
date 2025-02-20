# Assignment-11

% Parameters
L = 0.75;       % Length of rod (m)
dx = 0.025;     % Spatial step size (m)
dt = 0.00015;   % Time step size (s)
k = 1;          % Thermal conductivity (W/m°C)

% Discretization
x = 0:dx:L;     % Spatial grid
T = zeros(1, length(x));  % Initial temperature profile
T(1) = 100;     % Boundary condition at x = 0
T(end) = 50;    % Boundary condition at x = L

% Number of time steps
num_steps = 500;

% Create figure for animation
figure;
axis tight manual;
xlabel('Position (m)');
ylabel('Temperature (°C)');
title('Temperature Profile Evolution');
grid on;

% Initialize plot with initial temperature profile
plot(x, T, 'LineWidth', 2);
ylim([min(T)-10, max(T)+10]);  % Set y-axis limits
pause(0.01);  % Pause to show initial plot

% Explicit finite difference method and animate
for n = 1:num_steps
    T_new = T;
    for i = 2:(length(x) - 1)
        T_new(i) = T(i) + k * dt / (dx^2) * (T(i+1) - 2*T(i) + T(i-1));
    end
    T = T_new;
    
    % Update plot with new temperature profile
    plot(x, T, 'LineWidth', 2);
    ylim([min(T)-10, max(T)+10]);  % Update y-axis limits
    title(sprintf('Temperature Profile at Time Step %d', n));
    drawnow;  % Update figure window
    
    % Pause to control animation speed
    pause(0.01);
end

% Final temperature profile plot
figure;
plot(x, T, 'LineWidth', 2);
xlabel('Position (m)');
ylabel('Temperature (°C)');
title('Final Temperature Profile');
grid on;
