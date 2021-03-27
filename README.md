import matplotlib.pyplot as plt
import math
import numpy as np
def frange(x, y, jump):
    while x < y:
        yield x
        x += jump
with open('results.xml', 'w') as f:
    xres = []
    fres = []
    for x in frange(-10, 10, 0.01):
        A = 1.34941
        b = (x*x+A*A) ** 0.5
        c = 100 - b / math.pi
        d = math.fabs(c)
        e = math.exp(d)
        g = math.sin(x) * math.sin(A)
        function = -0.0001 * (math.fabs(e*g) + 1) ** 0.1
        xres.append('%.4f' % x)
        fres.append('%.4f' % function)
    f.write('<?xml version="1.1" encoding="UTF-8" ?>\n')
    f.write('<data>\n')
    f.write('\t<xdata>\n')
    for i in range(len(xres)):
        f.write('\t\t<x>' + str(xres[i])+'</x>\n')
        f.write('\t<xdata>\n')
        f.write('\t<ydata>\n')
    for i in range(len(fres)):
        f.write('\t\t<y>' + str(xres[i]) + '</y>\n')
    f.write('\t<ydata>\n')
    f.write('</data>')
    f.close()
    fig = plt.figure()
    ax = fig.add_subplot(111)
    xres = list(map(float, xres))
    fres = list(map(float, fres))
    ax.set_xticks(np.arange(-10, 10, 1 ))
    ax.set_yticks(np.arange(min(fres), max(fres), 0.1))
    ax.plot(xres, fres)
    plt.show()
