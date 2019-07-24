1. 页面跳转后返回到页面上方
~~~
router.afterEach((to,from,next) => {
  window.scrollTo(0,0);
})
~~~