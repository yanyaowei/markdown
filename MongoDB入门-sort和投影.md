##### //查询文档时，默认按下划线_id的值进行升序排列

db.emp.find();

##### //排序函数sort()可以用来指定文档的排序规则,sort中需要传递一个对象来指定排序规则

db.emp.find({}).sort({sal:1});

##### //1表示升序，-1表示降序

db.emp.find({}).sort({sal:-1});

##### //下面这个表示：先按sal比较升序，之后有一样的话按empno降序

db.emp.find({}).sort({sal:-1,empno:-1});

##### //limit skip sort 可以用任意顺序调用，在用的时候是先调sort,再skip，再limit

##### //查询时，可以在第二个参数的位置来设置查询结果，要什么显示就设置为1，不显示设置为0

db.emp.find({},{ename:1,_id:0});