## python 鼠标右键点击描点，滚轮放大缩小
    fig = plt.figure()
    ax1 = plt.subplot(111)
    ax1.plot(x,y)
    def call_back(event):
        axtemp = event.inaxes
        if not axtemp:
            return
        x_min, x_max = axtemp.get_xlim()
        fanwei = (x_max - x_min) / 10
        if event.button == 'up':
            ax1.set(xlim=(x_min + fanwei, x_max - fanwei))
            ax2.set(xlim=(x_min + fanwei, x_max - fanwei))
            ax3.set(xlim=(x_min + fanwei, x_max - fanwei))
            ax4.set(xlim=(x_min + fanwei, x_max - fanwei))
            print('up')
        elif event.button == 'down':
            ax1.set(xlim=(x_min - fanwei, x_max + fanwei))
            ax2.set(xlim=(x_min - fanwei, x_max + fanwei))
            ax3.set(xlim=(x_min - fanwei, x_max + fanwei))
            ax4.set(xlim=(x_min - fanwei, x_max + fanwei))
            print('down')
        elif event.button == 3:
            axtemp.scatter(event.xdata, event.ydata, s=10, color='black', marker=',')
            axtemp.annotate('{0:.3f},{1:.3f}'.format(event.xdata, event.ydata), xy=(event.xdata, event.ydata))
        fig.canvas.draw_idle()  # 绘图动作实时反映在图像上

    fig.canvas.mpl_connect('button_press_event', call_back)
    plt.show()


## 让子图都能做同一个操作，单个子图放大，所有子图都进行放大
    from matplotlib import pyplot as plt
    ax1 = plt.subplot(2,1,1)
    ax1.plot(...)
    ax2 = plt.subplot(2,1,2, sharex=ax1)
    ax2.plot(...)
## 字典转对象
    def dic2obj(d):
        top = type('new', (object,), d)
        seqs = tuple, list, set, frozenset
        for i, j in d.items():
            if isinstance(j, dict):
                setattr(top, i, dic2obj(j))
            elif isinstance(j, seqs):
                setattr(top, i, type(j)(dic2obj(sj) if isinstance(sj, dict) else sj for sj in j))
            else:
                setattr(top, i, j)
        return top
