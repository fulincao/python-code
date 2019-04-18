## python 鼠标点击描点
    fig = plt.figure()
    ax1 = plt.subplot(111)
    ax1.plot(x,y)
    def call_back(event):
        info = 'name:{}\n button:{}\n x,y:{},{}\n xdata,ydata:{} {}'.format(event.name, event.button, event.x, event.y,event.xdata, event.ydata)
        ax = event.inaxes
        ax.scatter(event.xdata, event.ydata, s=15, color='black', marker=',')
        ax.annotate('{0:.3f},{1:.3f}'.format(event.xdata, event.ydata), xy=(event.xdata, event.ydata))
        fig.canvas.draw_idle()

    fig.canvas.mpl_connect('button_press_event', call_back)
    plt.show()
