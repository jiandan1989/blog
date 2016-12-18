title: Javascript设计模式
date: 2016-12-18 17:53:36
tags:
---
#### 简单工厂模式

简单工厂模式(Simple Factory)又叫静态工厂模式，由一个工厂对象决定创建某一种产品对象类的实例，主要用来创建同一类对象

小白经过几天对团队代码的学习，终于对面向对象思想有所认知，自己跳动的小心脏跃跃欲试，信心满满准备大显身手...

- 工作中的第一次需求

<!--more-->

"小白，这几天学习的怎么样?登录模块的需求你能来处理一下么?"项目经理问

"没问题，" 小白答道

"不过用户名输入框这里如果用户输入的内容不符合规范就自定义个警示框警示一句'用户名不能多于16个字母或数字'"

"好的" 于是小白简简单单的写下了一个警示框类

         var LoginAlert = function(text){

           this.content = text;
        }
         LoginAlert.prototype.show = function(){

            //显示警示框

         }

           var userNameAlert = new LoginAlert('用户名不能多于16个字母或数字');

           userNameAlert.show();


"关于用户输入的密码也有一个需求，就是当用户输入的密码错误时也提示一句，输入的密码不正确的提示文案吧"

"没问题" 小白心中安息，面向对象编程就是好用，这不刚写完的类，这么快就用上了'小case'

    var passwordAlert = new LoginAlert('输入的密码不正确');

"小白，用户登录时如果用户名不存在你提示一句'您的用户名不存在，请重新输入'"

"没问题"，小白心中暗喜

"不过这里有些变化，就是要在警示框中添加一个注册按钮"

"添加一个按钮...."，小白傻眼了，心想"以前的功能这可怎么服用啊 哎，又得创建一个类了"


        var loginConfirm = function (text) {
            this.content = text;
        }

        loginConfirm.prototype.show = function () {
            //显示警示框
        }

        var loginFailConfirm = new LoginConfirm('您的用户名不存在，请重新输入');

        loginFailConfirm.show();

"小白"，登录成功后给出一个自定义提示框，处理有 确定取消按钮，也提示一句"欢迎回来，请输入您今天的心情吧"

"这又是一个心累..."，小白感叹道，于是只好添加一个类

        var LoginPrompt = function (text) {
            this.content = text;
        }

        LoginPrompt.prototype.show = function () {
            //显示提示框
        }

利用了大半天事件，小白终于把这些需求写完了

"小明。注册模块你来做吧，当用户输入的新用户名规范不正确的时候提示，用户名不能多于16个字母或数组，当用户输入的两次密码不正确时提示，'您两次输入的密码不同意，请重新输入，当用户的邮箱不规范时提示。。。。'",项目经理吩咐着小明余下的工作

"项目经理，登录模块谁做的，里面是不是也有提示框之类的需求啊?" 小明问项目经理

"小白负责的，不过他那里的情况要逼着还多几种"。

"好的"于是小明找来小白"小白，你写了登录模块，把你写的方法借我用一下。"

"好呀，我是通过对类实例化对象实现的"。小白回应道

"那太好了，我这边就可以无缝使用了，快给我"

##### 如果类太多，那么提供一个

于是小白将LoginAlert、LoginConfirm、LoginPrompt3个类告诉了小明

"怎么这么多？还是以以前Login为前缀，这样吧，你写个简单工厂给我吧"

"简单工厂，这是什么？" 小白好奇问

"这是一种模式啊，我的意思是说你给我3个类，在每次创建时还要找到相应的类，太麻烦了，而且在注册(regist)模块用你的login前缀也不太好，所以你最好封装在一个函数里，这样我只需要记住这个函数，然后通过这个函数就可以创建我需要的对象为我所用岂不是更好，
这样不但是我，而且其他人都不用再关注创建这些对象到底依赖于哪个基类了，而我们知道这个函数就可以了，这个函数通常也被称为工厂函数，这种模式也叫简单工厂模式，它是工厂模式中最简单的一种形式，你看它很像一个会变戏法的魔法师，你想要魔法师为你变得礼物
不过你不需要知道魔术师是用什么变得，你只需要知道有这位魔法师就行，然后找他就能帮你得到你想要的东西"

"原来是这样，可是我该如何改呢？"

"举个例子，比如说体育商品店卖体育器材，里面有很多体育用品，及其相关介绍等，当你来到体育用品店买一个篮球及其相关介绍时，你只需要问售货员，他会帮你找到你所要的东西"

        //篮球基类
        var Basketball = function () {
            this.intro = "篮球盛行于美国";
        };

        Basketball.prototype = {
            getMember: function () {
                console.log('每个队伍需要5名队员');
            },
            getBallSize: function () {
                console.log('篮球很大');
            }
        };
        //足球基类

        var Fallboll = function () {
            this.intro = "足球在世界范围内很流行";
        };

        Fallboll.prototype = {
            getMember: function () {
                console.log('每个队伍需要11名队员');
            },
            getBallSize: function () {
                console.log('足球很大');
            }
        };

        //网球基类

        var Tennis = function () {
            this.intro = "每年有很多网球系列赛";
        };

        Tennis.prototype ={
            getMemeber:function () {
                console.log('每个队伍需要1名队员');
            },
            getBallSize:function () {
                console.log('网球很小');
            }

        };

        //运动工厂

        var SportFactory = function (name) {
            switch (name){
                case 'NBA':
                    return new Basketball();
                case 'wordCup':
                    return new Fallboll();
                case 'FrenchOpen':
                    return new Tennis();
            }
        }

"当你想和小伙伴踢足球，只需要告诉电源我要买个足球即可，你使用这个商店工厂时仅仅需要记住SportFactory这个工厂对象就好了，这个工厂魔术师会帮你找到你需要的一切"

        //为世界杯创建一个足球，只需要记住运动工厂SportFactory，调用并创建

        var football = SportFactory('wordCup');

        console.log(football);
        console.log(football.intro);

        football.getMember();

"很简单，好了去把你的代码改一下吧，别忘了告诉我你创建的那位'魔术师'";

很快小白就把自定义弹框这位'魔术师'，请来了


        var PopFactory = function (name) {
            switch (name) {
                case 'alert':
                    return new LoginAlert();
                case 'confirm':
                    return new LoginConfirm();
                case 'prompt':
                    return new LoginPrompt();
            }
        }

"很不错"，小明夸道，然后又看了看小白之前写的LoginAlert、LoginConfirm、LoginPrompt3个类，皱了一下眉头，说"这三个类有很多地方是相同的，是可以抽象出来共用的",你也可以用简单工厂的方式实现他们

#### 一个对象有时也可以替代很多类

"这怎么实现?",还是跟上面一样的结构? 小白很惊讶

"不太一样，详细跟你说一下吧，简单工厂模式的理念就是创建对象，像上面那种方式是对不同的类实例化，不过除此之外简单工厂还可以用来创建相似的对象，而你创建的3个类很多地方都比较相似，比如都有关闭按钮，
都有提示文案等，所以你可以通过将这些相似东西提取，不相似的针对性处理即可，这有点类似我们之前学习继承时的寄生模式，很想，但是又不太一样，因为这里没有父类，所以无需做任何继承，
你只需要创建一个对象即可，然后通过对这个对象大量拓展方法和属性，并在最终将对象返回出来。"

"举个例子,比如你想创建一些书，那么这些书都有一些相似的地方，比如目录、页码等，也有一些不相似的地方，如书名、出版时间、书的类型等，对于创建的对象相似的属性好处理，对于不同的属性就要针对性的进行处理了，比如我们
将不同的属性作为参数传递进行处理"



        //工厂模式

        function createBook(name,time,type) {
            var o = {};

            o.name = name;

            o.time = time;

            o.type = type;

            o.getName = function () {

                console.log(this.name);

            }

            return o ;//将对象返回
        }

        var book1 = createBook('js book',2014,'js');

        var book2 = createBook('css book',2013,'css');

        book1.getName();

        book2.getName();


"真的很像寄生式继承，只不过这里的o没有继承任何类或对象"

"所以你这3个类要改成一个工厂模式也就很简单了，首先抽象他们的相同点，比如公有属性this.content，原型公有方法show，当然也有不同点，比如确认框与提示框的确定按钮，比如提示框的用户输入框等等，所以你就可以像下面这样创建了"


        function createPop(type,text) {
            //创建一个对象，并对对象拓展属性和方法

            var o = {};

            o.content = text;

            o.show = function () {
                //显示方法
            };
            if(type == "alert"){
                //警示框差异部分
            }
            if(type == "prompt"){
                // 确认框差异部分
            }

            if(type == "confirm"){
                //确认框差异部分
            }
            //将对象返回
            return o ;
        }
        //创建警示框

        var userNameAlert = createPop('alert','用户名只能是26个字母和数字');

#### 你的理解决定你选择的方式


"但是小白这两个'魔术师'工厂还是有一定区别的，好好想一想，你知道是什么吗？"小明问

"第一种是通过类实例化对象创建的，第二种是通过创建一个新对象然后包装增强其属性和功能来实现的，他们之间的差异性也造成前面通过类创建的对象，如果这些类继承同一个父类，那么他们的父类原型上的方法是可以共用的
，而后面寄生方式创建的对象都是一个新的个体，所以他们的方法就不能共用了，当然选择哪种工厂方式来实现你的需求还要看你是如何分析你的需求的。"

--------

#### 工厂模式方法

工厂方法模式(Factory Method):通过对产品类的抽象使其创建业务主要负责用于创建多累产品的实例

广告是公司主要的一个经济来源，这不，很多企业等着要来公司首页打广告呢？

###### 广告展现

"小白，咱们新来了一批广告资源需求要投放，关于计算机培训的，一批是java的，用绿色字体，还有一批是PHP的，要用黄色字体，红色背景"

"没问题，于是小白准备创建两个雷，然后通过实例对象方式来完成这个需求"。

        var Java = function (content) {
            //将内容保存在content里面以备日后使用
            this.content = content;
        //    创建对象时，通过闭包，直接执行，将内容按需求的样式插入到页面内

            (function (content) {
                var div = document.createElement('div');
                div.innerHTML = content;
                div.style.color = 'green';
                document.getElementById('container').appendChild(div);
            })(content);
        };

        //创建PHP学科类

        var Php = function (content) {
            this.content = content;
            (function (content) {

                var div = document.createElement('div');
                div.style.color = 'yellow';
                div.style.background = 'red';
                document.getElementById('container').appendChild(div);
            })(content)
        }

刚写完就听到身后的喊声:"小白，又来了一批广告，关于javascript的，需求背景色是粉色...."

"好吧" 突然间小白想起昨天学习的简单工厂模式，心想"正好排上用场了"，就用简单工厂模式去实现吧，这样日后再创建对象直接找工厂就好了

        //创建java类

        var Java = function (content) {
          //..........
        };

        //创建PHP学科类

        var Php = function (content) {
            //...
        };

        //创建javascript学科
        var Javascript = function (content) {
            this.content = content;

            (function (content) {
                var div =document.createElement('div');
                div.innerHTML = content;
                div.style.color = "pink";
                document.getElementById('container').appendChild(div);
            })(content);
        };

        //学科类工厂

        function JobFactory(type,content) {
            switch (type){
                case 'java':
                    return new Java(content);
                case 'php':
                    return new Php(content);
                case 'javascript':
                    return new Javascript(content);
            }
        };

然后写了一个测试案例:

        JobFactory('Javascript','Javascript哪家强');

"小白，又来了一批UI学科，红色边框...."

小白沉默了。。。。

#### 方案的抉择

小明见状走路过来，"怎么了，小白？"

"需求总是在变，我不知道那种解决方式更好，开始需求简单，我就直接创建对象，后来需求多了，我就用简单工厂模式重构，而现在又变了，我不仅仅要添加类，还要修改工厂函数，而我更担心的是未来的需求还会变"

"这样啊"，小明微笑了以下，"不用担心，需求变是正常的，而我们还有更好的模式可以应用，刚才你用简单工厂模式遇到的问题就是每添加一个类就要修改两处是吧，所以说你可以使用以下工厂方法模式，这样以后每需要一个类，你只需要添加这个类就行，其他的不用操心了"

"工厂方法？" 这是一个什么样的模式？

"工厂方法模式本意是说将实际创建对象工作推迟到子类当中，这样核心类就成了抽象类，不过对于javascript不必这么深究，Javascript没有像传统创建抽象那样的方式轻易创建抽象类，所以在
javascript中实现工厂方法模式我们只需要参考它的核心思想即可，所以我们可以将工厂方法看做是一个实例化对象的工厂类，安全起见，我们采用安全模式类，而我们将创建对象的基类放在工厂方法类的原型中即可"

#### 安全模式类

小白有些不懂，打断小明的话:"小明，什么叫安全模式类，你说的我不是很懂，你能详细说明一下吗？"

"安全模式类是说可以屏蔽使用者对类的错误使用造成的错误，比如对于一个类(我们暂且称之为Demo类)的创建，我们知道类的前面是需要new关键字的(比如var d = new Demo())。不过如果其他人不知道这个对象(Demo)
是一个类，那么在使用时很可能忽略new 关键字直接执行类，(比如 var d = Demo())，此时我们得到的并不是我们预期的对象，如下所示:"


        var Demo = function () {

        };

        Demo.prototype = {
            show :function () {
                console.log('成功获取')
            }
        }

        var d = new Demo();

        d.show();//成功获取

        var d = Demo();

        d.show();//Uncaught TypeError : cannot read property 'show' of undefined

"那么你所说的安全模式就是为了解决这种问题吧"

"当然，，这也是避免想你一样的那些新来同学可能犯的错误，当然解决方案很简单，就是在构造函数开始时先判断当前对象this指代是不是类(Demo)，如果是则通过new关键字创建对象，如果不是
说明类在全局作用域中执行，(通常情况下)那么既然在全局作用域中执行当然this就会指向window了，(通常情况下，如非浏览器环境可为其他全局对象)，作用我们就要重新返回新创建的对象了 "


        var Demo = function(){

            if(!this instanceof Demo){

                return new Demo();

            }
        }

        var d = Demo();

        d.show();//成功获取

"有了安全模式我们就可以将这种技术应用在我们的工厂方法中了"


#### 安全的工厂模式

        //安全模式创建的工厂类e

        var Factory = function (type, content) {
            if (this instanceof Factory) {
                var s = new this(type, content);
                return s;
            }else {
                return new Factory(type,content);
            }
        };

        //工厂原型中设置创建所有类型数据对象的基类

        Factory.prototype = {
            Java:function (content) {

            },
            Php:function (content) {

            },
            Javascript:function (content) {

            },
            UI:function (content) {
                this.content = content;
                (function (content) {
                    var div = document.createElement('div');
                    div.innerHTML = content;
                    div.style.border = '1px red solid';
                    document.getElementById('container').appendChild(div);

                })(content);
            }
        }


"这样我们以后如果想添加其他类时，是不是只需卸载Factory这个工厂类的原型里面就可以了"

"恩，是这样，你再也不必担心创建时做任何修改，就好比在Factory类的原型里面注册了一张名片，以后需要那类直接拿着这张名片，查找上面的信息就能找到这个类了，所以你就不用担心使用时找不到基类的问题了"

"小白，这里是我们今天要添加广告的数据，给你，现在就给添加上吧，" 经理走过来对小白说。


            var data = [{
                type: "Java", content: "Java哪家强"
            }, {
                type: "Javascript", content: "Javascript哪家强"
            }, {
                type: "PHP", content: "PHP哪家强"
            }, {
                type: "UI", content: "UI哪家强"
            }];

小白接过数据一看，格式很友好，于是很快完成了经理提出的需求。

            for(var i = 0 ; i < data.length;i ++){
                Factory(data[i].type,data[i].content)
            }

"小白，广告那边又来了需求，需要一批C++学科，蓝色字体。。。。"

小白听到，笑了笑。。。




--------

#### 抽象工厂模式

--------

#### 建造者模式

--------

#### 原型模式

--------

#### 单例模式

-------

#### 外观模式

****

#### 适配器模式

--------

#### 代理模式

--------

#### 装饰者模式

--------

#### 桥接模式

--------

#### 组合模式

--------

#### 享元模式

--------

#### 模板方法模式

--------

#### 观察者模式

--------

#### 状态模式

--------

#### 策略模式

--------

#### 职责链模式

--------

#### 命令模式

--------

#### 访问者模式

--------

#### 中介者模式

--------

#### 备忘录模式

--------

#### 迭代器模式

--------

#### 解释器模式

--------

#### 链模式

--------

#### 委托模式

--------

#### 数据访问对象模式

--------

#### 流模式

--------

#### 简单模板模式

--------

#### 惰性模式

--------

#### 参与者模式

--------

#### 等待者模式

--------

#### 同步模块模式

--------

#### 异步模块模式

--------

#### Widget模式

--------

#### MVC模式

--------

#### MVP模式

--------

#### MVVM模式




