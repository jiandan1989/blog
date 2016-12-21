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

##### 分即是合---建造者模式

<b>建造者模式(Builder):</b>将一个复杂对象的构建曾与其表示层相互分离，同样的构建过程可采用不同的表示。

小白这几天对工厂模式学习让其认为创建任何对象只需要工厂模式就可以了，这不小明临时接到在页面发布用户简历的需求，来看看他们的对话吧。

###### 发布简历

"小明，还在加班呢？什么事情这么忙？" 小白问

"这不，刚接到任何，有一些找工作的人，想借助咱们的网站发布自己的简历。"

"哦，人很多么，都有什么要求？要不要我帮你选选啊？" 小白问

"不用，不是咱们公司招聘，是将它们简历向外推销，不过街道的简历还真不少，但是这些简历有一个要求，处理可以将它们的星期爱好以及一些特长发布在页面里，其他信息，如他们的练习方式，不要发布在网站上，要让需求公司来找咱们，不过话又说回来，他们想找的工作室可以分类的，比如对于喜欢编程的人来说他们要找的职位就是工程师"
了，当然这里可能还有一些描述，比如'每天沉醉于编程。。。。。'"

"听上去还想要分很多部分，这样创建他们要写不少工厂方法吧？" 小白问

"恩，很多部分需要抽象提取，不过首先要明确创建内容，比如创建用户信息如用户姓名等要读里处理，因为他们是要隐藏显示的，比如这些应聘者也要独立创建，因为他们代表一个整体，还有这些工作职位也要独立创建，他们是应聘者拥有的一部分，而且种类很多。"

"不过这样一来你需要创建的东西就多了，不仅仅应聘者需要创建，每位应聘者的信息，应聘职位都要创建，不过我想这几天我们讨论的创建模式好像的那个都不太适合你的需求啊" 小白道

###### 创建对象的另一种形式

"所以我不准备用任何工厂模式了，我想建造者模式更适合吧"

"建造这模式？这是一个新模式，以前还从未听蜀国，它与学过的几类工厂模式之间有区别么？"

"工厂模式主要是为了创建对象实例或者类族(抽象工厂)，关心的是最终产出(创建)的是什么，不关心你创建的整个过程，仅仅需要知道你最终创建的结果，所以通过工厂模式我们得到的都是对象实例或者类族，然而建造折磨而是在创建对象时要更为复杂一些，虽然其目的也是为了创建对象，但是它更关心的是创建这个对象的整个过程，甚至于创建对象的每一个细节，比如创建一个人，我们创建的结果不仅仅要得到人的实例，还要关注创建人的时候，这个人应该穿什么衣服，男的还是女的，兴趣爱好是什么。所以说建造者模式更注重的是创建的细节，而在本例中我们看到，我们需要的不仅仅是应聘者的一个实例，还要在创建过程中注意一下这位应聘者都有哪些兴趣爱好、他的姓名等信息，他所期望的职位是什么，等等，那么这些关注点都是需要我们创建的。"


        //创建一位人类

        var Human = function (param) {
            //创建技能
            this.skill = param && param.skill || '保密';
            //兴趣爱好
            this.hobby = param && param.hobby || '保密';

        }
        //类人原型方法
        Human.prototype = {
            getSkill: function () {
                return this.skill;
            },
            getHobby: function () {
                return this.hobby;
            }
        };
        // 实例化对象

        var Named = function (name) {
            var that = this;

            //构造器
            //构造函数解析姓名的姓和名

            (function () {
                that.wholeName = name;
                if (name.indexOf(' ') > -1) {
                    that.FirstName = name.slice(0, name.indexOf(' '));
                    that.secondName = name.slice(name.indexOf(' '));
                }
            })(name, that);
        }

        //实例化职位类

        var Work = function (work) {
            var that = this;
            //构造器
            // 构造函数中通过传入的职位特征来设置响应职位的描述
            (function (work, that) {
                switch (work) {
                    case "code":
                        this.work = '工程师';
                        that.workDescript = '每天沉醉于编程';
                        break;
                    case "UI":
                    case "UE":
                        that.work = "设计师";
                        that.workDescript = '设计更似一种艺术';
                        break;
                    case "teach":
                        that.work = "教师";
                        that.workDescript = "分享也是一种快乐";
                        break;
                    default:
                        that.work = work;
                        that.workDescript = "对不起，我们还不清楚您所选择职位的相关描述";
                }

            })(work,that);
        }

        //更换期望的职位

        Work.prototype.changeWork = function (work) {
            this.work = work;
        }
        //添加对职位的描述
        Work.prototype.cahgneDescript = function (setence) {
            this.workDescript = setence;
        }


###### 创建以为应聘者

"这样我们就创建了了抽象出来的3个类----应聘者，姓名解析类与期望职位类，然而创建应聘者类有些特殊，因为对其类闯入的参数做了一个小处理，就是&&与||的运用，如例子中的this.skill = param && param.skill ||'保密'表示，如果存在param这个参数，并且param拥有skill属性，就用这个属性复制给this的skill属性，否则将用默认值'保密来设置，'" 小明接着说："我们最终的目的是要创建以为应聘者，所以需要上面抽象的3个类，这样我们写一个建造者类，在建造者类中我们要通过对这3个类组合调用，就可以创建出一个完整的应聘者对象"


            /**
             - 应聘者建造者
             - 参数 name :姓名
             - 参数 work :期望职位
             - ***/
            var Person = function (name,work) {
                //创建应聘者缓存对象
                var _person = new Human();
                // 创建应聘者姓名解析对象
                _person.name = new Named(name);
                //创建应聘者期望职位
                _person.work = new Work(work);
                //将创建的应聘者对象返回
                return _person;
            };

"在应聘者建造者中我们分成三个部分来创建以为应聘者对象，首先创建一位应聘者缓存对象，缓存对象需要修饰(添加属性和方法)，然后我们向缓存对象添加姓名，添加一个期望职位，最终我们就可得到以为完整的应聘者了，看"

> var person = new Person('小明','code');

你可以来测试一下看看

>console.log(person.skill);//保密
>console.log(person.name.FirstName);//小
>console.log(person.work.work);//工程师
>console.log(person.work.workDescript);//每一天在编程汇总度过    
>person.work.chagneDescript('更改一下职位描述');//
>console.log(person.work.workDescript);//更改一下职位描述

"小白,看过之后在回顾下工厂模式，你感觉最大的感受是什么?"

"正向你说的那样，以前工厂模式创建出来的是一个对象，他追求的是创建的结果，别无他求，所以那仅仅是一个实实在在的创建过程，而建造者模式就有所不同，它不仅仅可得到创建的结果，然而也参与了创建的具体过程，对于创建的具体实现的细节也参与了干涉，可以说创建的对象更复杂，或者说这种模式创建的对象是一个符合对象"

###### 忆之获

回忆我们前面学过的集中工厂模式，他们都有一个共同特定，就是创建的结果都是一个完整的个体，我们对创建过程不得而知，我们只了解得到的创建结果对象，而在建造者模式中我们关心的是对象闯将过程，因此我们通常将创建对象的类模块化，这样被创建的类的每一个模块都可以得到灵活的运用于高质量的复用，当然我们最终的需求是要得到一个完整的个体，因此在拆分创建的整个过程，我们将得到一个统一的结果

当然这种方式对于整体对象类的拆分无形中增加了结构的复杂性，因此如果对象力度很小，或者模块间的复用率很低并且变动不大，我们最好还是要创建整个对象。

--------

#### 原型模式

#### 语言之魂---原型模式

<b>原型模式(prototype):</b>用原型实例指向创建对象的类，使用于创建新的对象的类共享原型对象的属性以及方法。

随着web的发张，产品经理对网页特效的追求越来越多，这不，经理让小白加快页面多种焦点图特效的研发呢

###### 语言中的原型

"小明，有个问题我一直没想明白" 小白说

“怎么了?” 小明问道

"你看，在Javascript中的继承是靠原型链实现的，那么这就是Javascript中的原型模式吧?"

"原型模式你都知道，看来你知道的只是还真不少，原型模式就是将原型对象指向创建对象的类，使这些类共享原型对象的方法与属性，当然Javascript是基于原型链实现对象之间的继承，这种继承是基于一种对属性或者方法的恭喜当，而不是对属性和方法的复制。"

###### 创建一个焦点图

"举个例子，假设页面中有很多焦点图(网页中很常见的一种图片轮播，切换效果)，那么我们要实现这些焦点图最好的方式就是通过创建对象来一一实现，所以我们就需要有一个焦点图类，比如我们把这个类定义为LoopImages"

        var LoopImages = function(imgArr,container){
            this.imgArr = imgArr;//轮播图片数组
            this.container = container;//轮播图片容器
            this.createImage = function(){} ;// 创建轮播图片
            this.changeImage = function(){};//切换下一张图片

        }

"如果一个页面中有多个这类焦点图，其切换动画一般是多样化的，有的可能是上下切换，有的可能是左右 切换，有的可能是渐隐切换，有的可能是放缩切换，等等因此创建的轮播图片结构应该是多样化的，同样切换的小果果也应该是多样化的，因此我们应该抽象出一个积累，让不同特效类去继承这个积累，然后对于差异化的需求通过重写这些继承下来的性或者方法来解决，当然不同的子类之间可能存在不同的街头样式，比如有的包含一个左右切换箭头，于是我们有了下面的例子"
    
        var SliderLoopImg = function (imgArr,container) {
            //构造函数继承图片轮播类
            LoopImgs.call(this,imgArr,container);
            //重写继承的切换下一张图片方法
            this.changeImage= function () {
                console.log('slideLoopImg changeImage function');
            }
        }
        //渐隐切换类

        var FadLoopImg = function (imgArr,container,arrow) {
            LoopImage.call(this,imgArr,container);
            //切换箭头私有变量

            this.arrow = arrow;
            this.chagneImage = function () {
                console.log('FadeLoopImg changeImage function');
            }
        }

我们创建一个显隐轮播图片测试实例很容易

        <!-- 实例化一个渐隐切换图片类 -->
        var fadeimg = new FadLoopImg([
            '01.png',
            '02.png',
            '03.png'
        ],'slide',['left.pn','right.png'])

        fadeimg.changeImage();//FadLoopImg changeImage function

"恩，用这种方式实现这类需求是极好的，" 小白说

###### 最优的解决方案

"是啊，像你这样刚来的同事如果能写出这样的代码已经很不错了，，不过还是存在一些问题的，首先我们看基类，作为基类是要被子类继承的，那么此时将属性和方法都写在基类的构造函数里会有些问题，比如每次子类继承都要创建一次父类，加入父类的构造函数中创建时存在很多耗时较长的逻辑，或者说每次初始化都做一些重复的东西，这样的性能消耗还是蛮大的，为了提高性能，我们需要有一种共享机制，这样每当创建基类时，对于每次创建的一些简单而产异化的属性我们可以放在构造函数中，而我们将一些消耗资源比较大的方法放在基类的原型中，这样就会避免很多不西药的消耗，这也就是原型模式的一个出行，这一模式很想我们之前提到过的累积成，都是基于原型链，也由于这种类型很常见，所以我们进场护士这种模式，在其他面向对象语言中，之所以这种模式经常被提到，是以为该模式在实现这种'共享'上要麻烦一些，是通过复制完成的，我们这个例子该如何修改你知道了吧"

小白思考了一下"原型模式就是将可服用的、可共享的、耗时大的从基类中提出来然后放在其原型中，然后子类通过组合继承或者寄生组合式继承而将方法和属性继承下俩，对于子类中那些需要重写的方法进行重写，这样子类创建的对象既具有子类的属性和方法也共享了基类的原型方法，像下面这样"

        //图片轮播类
        var LoopImages = function (imgArr, container) {
            this.imagesArray = imgArr;  //轮播图片数组
            this.container = container;//轮播图片容器
        }
        LoopImages.prototype = {
            //创建轮播图片
            createImage:function () {
                console.log('loopimage createImage function');
            },
            //切换下一张图片
            chagneimage:function () {
                console.log('Loopiamges changeimage function');
            }
        }
        //上下滑动切换类
        var SlideLoopImg = function (imgArr, container) {
            //构造函数继承图片轮播类
            LoopImages.call(this,imgArr,container);
        }
        SlideLoopImg.prototype = new LoopImages();
        //重写继承的切换下一张图片方法
        SlideLoopImg.prototype.changeImage = function () {
            console.log('SlideImage changeimage function');
        };
        //渐隐切换类

        var FadeLoopImg =function (imgArr,container,arrow) {
            LoopImages.call(this,imgArr,container);
            //带有箭头私有变量
            this.arrow = arrow;
        }
        FadLoopImg.prototype = new LoopImages();
        FadLoopImg.prototype.changeImage = function () {
            console.log('FadeLoopImg changeImage function');
        }

        //测试用例

        console.log(fadeImg.container)//slide
        fadeImg.changeImage();//FadeLoopimg changeImage function

###### 原型的拓展

"恩，很不错不过小白，你知道原型模式还有一个特定么"

"给点提示呗，关于子类还是父类的" 小白笑着问道

"都有，不过确切的话是关于原型对象的"

“原型对象？”

“原型对象是一个共享的对象，那么不论是父类的实例对象或者是子类的继承，都是对他的一个指向引用，所以原型对象才会被共享，既然被共享，那么对原型对象的拓展，不论是子类或者父类的实例对象都会继承下来，小编你可以试一试”

        LoopImages.prototype.getImageLength = function(){
            return this.imageArray.length;
        }
        FadeLoopimg.prototype.getContainer= function(){
            return this.container;
        }
        console.log(fadeImg.getImageLength())
        console.log(fadeImg.getContainer())

"真的是这样啊，" 小白兴奋的说

"所以说原型模式有一个特点就是在任何时候都可以对基类或者子类进行方法的拓展，而且所有被实例化的对象或者类都能获取这些方法，这样给予我们队功能拓展的自由性，但是有一点你要注意，正式由于这种方式太自由了，所以不要随意去做，否则如果修改类的其他属性或者方法很有可能影响其他人"

"恩，不过真的感觉原型继承模式好强大" 小白感叹道

那是当然，所以说这种模式Javascript语言的灵魂，在Javascrit中又喝多面向对象编程思想或者设计模式都是基于原乡模式继承实现的

'看开原型模式真的很重要' 小白说

##### 原型继承

"不过原型模式更多的使用在对对象的创建上，比如创建一个实例对象的构造函数比较复杂，或者耗时比较长，或者通过创建多个对象来实现，此时我们最好不要用new关键字去复制这些积累，到哪可以通过对这些对象属性或者方法进行复制来实现创建，这是原型模式的最初思想，如果涉及多个对象，我们也可以通过原型模式来实现对新对象的创建，那么首先要有一个原型模式的对象复制方法"

        /**
         - 基于已经存在的模板对象克隆出新对象的模式
         - argumets[0],arguments[1],arguments[2]:参数1，参数2，参数2表示模板对象
         - 注意，这里对模板引用类型的属性实质上进行了前复制(引用类型属性共享)，当然根据需求可以自行深复制(引用类型属性复制)
         - **/

        function prototypeExtend() {
            var F = function () {//缓存类，为实例化返回对象临时创建
                args = arguments;//模板帝乡参数序列
                i = 0;
                len = args.length;
                for(; i < len ; i ++){
                    //遍历每个模板对象中的属性
                    for(var j in args[i]){
                        //将这些属性复制到缓存类圆形中
                        F.prototype[j] = args[i][j];
                    }
                }
            }
            //返回缓存类的一个实例
            return new F();
        }

比如切游戏红我们创建一个企鹅对象，如果游戏后只能怪没有企鹅基类，只是听过了一些动作模板对象，我们就可以通过实现对这些模板对象的继承来创建一个企鹅实例对象

        
        var penguin = prototypeExtend({
            speed : 20,
            swim:function () {
                console.log('游泳速度' + this.speed);

            }
        },{
            run:function (speed) {
                console.log('奔跑速度' + speed);
            }
        },{
            jump:function () {
                console.log('跳跃动作')
            }
        });

既然通过prototypeExtend创建的是一个对象，我们就无需再用new去创建新的实例对象，我们可以直接使用这个对象
>penguin.swim();//游泳速度20
>penguin.run(10);//奔跑速度10
>penguin.jump();//跳跃动作

这又是一种继承的实现方式啊

#### 忆之获

原型模式可以让多个对象分享同一个原型对象的属性与方法，这也是一种继承方式不过这种继承的实现是不需要创建的，而是将原型对象分享给那些继承的对象，当然有时需要让每个继承对象独立拥有一份原型对象，此时我们就需要对原型对象进行复制

由此我们可以看出，原型对象更适合在创建复杂的对象时，对于那些需求一直在变化而导致对象结构不停的改变时，将那些比较稳定的属性与方法共用而提取的继承的实现。

--------

#### 单例模式

##### 一个人的寂寞---单例模式

<b>单例模式(singleton):</b>又被称为单体模式，是只允许实例化一次的对象类，有时我们也用一个对象来规划一个命名空间，井井有条的管理对象上的属性与方法

这不，小白街道一个任务，公司要开展一个活动，经历让小白做一个宣传页面，这可是小白作为新人街道的第一个完整的项目哦，看看他是怎么做的吧

###### 滑动特效

"小白,你在活动页面实现新闻列表中实现的鼠标滑动特效怎么定义了这么多的方法"

        function g(id){
            return docuemnt.getElementById(id)
        }
        function css(id,key,value){
            //简单样式属性设置
            g(id).style[key] =value;
        }
        function attr(id,key,value){
            g(id)[key] = value;
        }
        function html(id,value){
            g(id).innerHTML = value;
        }
        function on(id,type,,fn){
            g(id)['on'+type] = fn;
        };

"这么左右什么不妥么？" 小白问

"你在页面中添加了很多变量， 比如你定义的绑定事件方法on，如果日后其他人要为你的页面添加需求，增加代码而定义一个on变量或者重写了on方法，这样就会和你的代码起冲突了，所以你最好要用单例修改一下你书写的代码"

##### 命名空间的管理员

"单例模式"小白有些疑惑,"你是说要把我定义的这些功能方法放在一个对象里么？"

"单例模式你没有用过么，这可能是javascript中最常见的一种模式了，这种模式经常为我们提供一个命名空间，如我们使用的Jquery苦，单例模式就为它提供了一个命名空间jQuery"

"命名空间"

"没听过么，明明空间就是人们所说的namespace，有人也叫它名称空间，它解决这么一类问题，为了让代码更易懂，人们常常用单词或者拼音定义变量或者方法，但由于人们可用的单词或者汉字拼音是有限的所以不同的人定义的变量使用单词名称很有可能重复，此时就需要用命名空间来月数每个人定义的变量来解决这类问题，比如小张写的代码，它可以定义个xiaozhang命名空间，这样以后使用小张定义的变量时就可以通过xiaozhang.xx"来使用，这样以，同理，小李定义了一个xiaoli命名空间，那么以后同样要使用xiaoli.xx访问小李定义的变量"

"啊这样啊，"小白似乎有些明白，我们要使用jquery定义animate方法我们就要用jquery.animate()来访问，这是同一个道理，对不对？“

"很聪明么，所以说单例模式常用来定义命名空间，所以你知道把你的代码怎么改了吧？"

"很容易，直接将上面的代码放在定义变量的{}里就可以了吧";
    
        var Ming = {
            g:function(id){
                return docuemnt.getElementById(id);
            },
            css:function(id,key,value){
                //简单样式属性设置
                g(id).style[key] = value;
            }
        }

"你别忘了，在你的css方法中你使用了g方法，而我们刚才说过，单例模式要想使用定义的方法一定要加上命名空间Ming，所以你不要忘记将css方法中的g方法改成Ming.g,由于g方法和css方法都在单例对象Ming中，也就是说这两个方法都是单例对象Ming的方法，而对象中this指代当前对象，所以我们还可以在css方法中通过this.g来使用Ming单例对象中的g方法"

        var Ming = {
            g:function(id){
                return docuemnt.getElementById(id);
            },
            css:function(id,key,value){
                this.g(id).style[key] = value;
            }
        };

真是大意了

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




