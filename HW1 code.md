import matplotlib.pyplot as plt
import numpy as np
import random
x = np.array([0, 1, 2, 3, 4], dtype=np.float32)
y = np.array([2, 3, 4, 5, 6], dtype=np.float32)
# x = np.array([0, 1, 2, 3, 4], dtype=np.float32)
# y = np.array([1.9, 3.1, 3.9, 5.0, 6.2], dtype=np.float32)

def predict(a, xt):
	return a[0]+a[1]*xt

def MSE(a, x, y):
	total = 0
	for i in range(len(x)):
		total += (y[i]-predict(a,x[i]))**2
	return total

def loss(p):
	return MSE(p, x, y)

def optimize():
    fail = 0
    p = [0.0, 0.0]
    h = 0.01
    while fail < 3000:
        fail += 1
        dx = random.uniform(-h, h)
        dy = random.uniform(-h, h)
        pxy = [p[0]+dx, p[1]+dy]
        if loss(pxy) == 0:
            p = pxy
            break
        elif loss(pxy) < loss(p): p = pxy
        else: continue

return p

p = optimize()

    # Plot the graph
y_predicted = list(map(lambda t: p[0]+p[1]*t, x))
print('y_predicted=', y_predicted)
plt.plot(x, y, 'ro', label='Original data')
plt.plot(x, y_predicted, label='Fitted line')
plt.legend()
plt.show()
