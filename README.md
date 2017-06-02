# Model

The model I used was the kinematic model with a state vector:

[x, y, psi, v, cte, epsi]

x = x + v * cos(psi)  
y = y + v * sin(psi)  
psi = psi + v / Lf *d * dt  
v = v + a + dt  
cte(t) = f(x(t)) - y(t)  
epsi(t) = psi(t) - psides(t)  


x(t+1) = x(t) + v(t) * cos(psi) * dt  
y(t+1) = y(t) + v(t) * sin(psi) * dt  
psi(t+1) = psi(t) + v(t) / Lf * d * dt  
v(t+1) = v(t) + a(t) * dt  
cte(t+1) = f(x(t)) - y(t) + (v(t) * sin(espi(t)) * dt)  
espi(t+1) = psi(t) - psides(t) + ((v(t) / Lf * d * dt))

# Timesteps

I picked an N of 10 and a dt of 0.05. I found that trying to
fit too far into the future yielded low results, that a lower
N and dt meaning we only try to fit up to the next 1/2 second.

# Latency

Latency was handled by guessing the state 100ms in the future
and using that as our base point for fitting a line. So our base
points weren't at (0, 0), but rather where we thought we would be
base on our current trajectory. The only problem with doing this is
that we assume a constant latency, while in the real world latency
would vary.
