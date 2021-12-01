> 使用Golang和heap实现一个通用的定时器模块，代码来自：https://github.com/xiaonanln/goTimer

// 一般上层模块需要在一个主线程的goroutine里按一定的时间间隔不停的调用Tick函数，从而确保timer能够按时触发，并且
// 所有Timer的回调函数也在这个goroutine里运行。
func Tick() {

}