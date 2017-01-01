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

### 模块分明

其实在Javascript中大力模式除了定义命名空间外，还有一个作用你需要知道，就是通过当里模式来管理代码库的各个模块，比如早起百度tangram，雅虎的YUI都是通过单例模式来控制自己的每个功能模块的，比如tangram中定义命名空间为百度，当添加设置元素class方法，插入一个元素方法是，他们会放到dom模块，当添加事件中阻止事件的冒泡方法，阻止事件的默认行为方法的时候，会放到Event模块里,当添加去除字符创首位空白字符方法将字符串进行html编码时，会放到string模块中....

>baidu.dom.addclass //添加元素类
>baidu.dom.apped //插入元素
>baidu.event.stopProgagation //阻止冒泡T
>baidu.event.trim //去除字符串首尾空白字符
>baidu.string.encodeHTML //将字符串进行html编码

#### 创建一个小型代码库

所以我们以后写自己的小型方法库的时候也可以用单例模式来规范我们自己代码库的各个模块，比如我们有一个A库，它包含共用模块，工具模块，ajax模块和其他模块，那么我们就可以自己定制一个如下的小型代码库

        var A = {
            Util : {
                util_method1:function(){},
                util_method2:function(){}
            },
            Tool:{
                tool1_method:function(){},
                tool2_method:function(){}
            },
            Ajax:{
                get:function(){},
                post:function(){}
            },
            others:{}
        }

那么我们想使用公共模块。工具模块，ajax模块方法时就像下面这样。

        A.Util.util_method1()
        A.Tool.tool1_method

#### 无法修改的静态变量

"看上去代码哭的结构真的很清晰了，大家使用起来更容易了"  小白说

"恩，这正是单例模式的好处，不过这是在对代码管理上，其实有一个功能用单例模式实现更适合，就是管理静态变量"

"静态变量，Javascript中不是没有静态变量么，" 小白追问

"你知道，Javascript根本没有static这类关键字，所以定义任何变量理论上都是可以更改的，所以在Javascript中实现创建静态变量又变的很重要，当然Javascript很灵活，人们根据静态变脸只能方位不能修改并且无创建后就能使用这一特点，想出来一个好主意，能访问的变量定义的方式有很多，比如定义在全局空间里，或者定义一个函数内部，并定义一个特权方法访问，等等，既然不能修改，定义在全局空间里就显得很不靠谱了，而如果将变量放在一个函数内部，那必须通过特权方法访问，如果我们不提供赋值变量的方法，值提供获取变量的方法，不就可以做到限制变量的修改并且可以供外界访问的需求了么？但是还有最后一个问题就是目前放在函数内部的变量还能供外界访问，为实现创建后就能使用这一需求，我们就需要让他创建的函数执行一次，此时我们创建的对象内保存静态变量通过取值器访问，最后将这个对象作为一个单例放在全局空间里作为静态变量单例对象共他人使用"

        var Conf = (function(){
                
                //私有变量
                var conf = {
                    MAX_NUM :100,
                    MIN_NUM :1,
                    COUNT:1000
                }
                //返回取值器对象
                return {
                    get:function(name){
                        return conf[name] ? conf[name] : null;
                    }
                }
            })();

"很奇妙啊，没有赋值器我们就不能修改内部定义的变量了那么我们想要使用创建了的静态变量，像下面这种方式就可以了吧" 小白说

        var count = Conf.get('COUNT');
        console.log(count);

#### 惰性单例

"不过为什么静态变量都是大写啊？"小白问

"这是一种定义习惯，在其他编程语言中静态变量都习惯大写，所以在Javascript中虽然是模拟的静态变量我们也要尊重这一使用习惯，有些时候对于单例对象需要延迟创建，所以在单例中还存在一种延迟创建的形式，有人也称之为'惰性创建'"

        //惰性载入单例

        var LazySingl = (function(){
            //单例实例引用
            var _instance = null;
            //单例
            function Single(){
                /*这里定义私有属性和方法*/
                return {
                    publicMethod:function(){},
                    publicProperty :1.0
                }
            }
             // 获取单例独享接口
             return function(){
                //如果为创建单例将创建单例
                if(!_instance){
                    _instance = Single();
                }
                return _instance;
             }
            })();

我们测试一下可以看出通过LazySingle对象可以成功获取内部创建的单例对象了

>console.log(LazySingle().publicProperty);//1.0

#### 忆之获

单例模式有时也被称为单体模式，它是一个值允许实例化一次的对象类，有时这么做也是为了节省系统资源，当然Javascript中单例模式经常作为命名空间来实现，通过单例对象我们可以将各个模块的代码井井有条的树立在一起

所以如果你想让系统中只存在一个对象，那么单例模式则是最佳解决方案


-------

#### 外观模式

外观模式(facade):为一组复杂的子系统接口提供一个更高级的统一接口，通过这个接口使得对字体通接口的访问更加容易，在javascript中有时也会用与对底层结构兼容性做同一个封装来简化用户使用。

前几天的对创建行的设计模式的学习使小白对对象的创建有了深入的理解，今天又了新的挑战，这不小白正在为页面写交互呢？

#### 添加一个点击事件

"小白，你为页面文档document对象绑定了一个click事件来实现隐藏提示框的交互功能，直接用click为document绑定的？" 小明过来问小白

"是这样，不过这有什么问题么？" 小白回答道

"你的功能是完成了，只不过。。。" 小明犹豫了以下

"怎么了。"

"我看一下你的代码"

        document.onclick = function(){
            e.preventDefault();
            if(e.target !== document.getElementById('myinput'));
            hidePageAlert();
        }

        function hidePageAlert(){
            //隐藏提示框
        }

"首先，你为document绑定了onclick事件，但是你知道onclick是DOM0级事件，也就是说这种方式绑定的事件相当于为元素绑定一个事件方法，所以如果我们团队中有人再次通过这种方式为document绑定click事件，就相当于重复定义了一个方法，会将你定义的click事件方法覆盖，如下列程序"

        document.onclick = function(){
            //其他开发人员重新为document绑定事件会覆盖前面定义的DOM 0 级click事件
        }

"所以你这种方式是很危险的，因此你应该用DOM2级事件吃力程序提供的方法addEventListener来是实现，然而你知道老版本的IE浏览器(低于9)是不支持这个方法的，所以你要用attachEvent，当然如果有不支持DOM2级事件处理程序的浏览器，你只能用onclick事件方法绑定事件"

"如此看来为元素绑定一个事件真不是一件容易的事，我们要做这么多的事情，有没有一个兼容所有浏览器的方式呢?" 小白问

#### 兼容方式

小明微笑道:"当然有了，我们可以用外观模式来封装他们，这就想每天中午我们急冲冲的去餐厅吃饭，人很多，不论是餐厅点餐员还是作为顾客的我们，大家都想尽量节约时间，以尽可能少的成本完成我们点餐吃饭的整个流程，所以通常的做法是去点套餐，这就很简洁明了，比如鱼香肉丝饭套餐，会为我们提供米饭、菜甚至饮料等。当然我们就不用再浏览遍历每一种菜，主食点什么，饮料要买哪种等，因为套餐已经为我们定制好了，那么在Javascript中也可以通过一个'套餐'来简化复杂的要求，比如我们统一功能接口方法的不同意，我们可以通过外观像点套餐那样定义一个统一接口方法，这样就提供了一更简单的高级接口，简化了我们队复杂的底层接口不统一的使用需求，根据这一思想我们就可以按照如下方式简化我们事件的绑定"

        //外观模式实现
        function addEvent(dom,type,fn){
            //对于支持DOM2 级事件处理程序addEventListener方法的浏览器
            if(dom.addEventListener){
                dom.addEventListener(type,fn,false);
            }else if (dom.attachEvent){
                //对于不支持addEventListener方法但支持attachEvent方法的浏览器
                dom.attachEvent('on' + type,fn)

            }else{
                //对于不止addEventListener方法也不支持attachEvent方法，但支持on + '事件名'的浏览器
                dom['on' + type ] = fn;
            }

"这样我们以后对于支持addEventListener或attachEvent方法的浏览器就可以放心的绑定多个事件了"

        var myInput = document.getElementById('myinput');
        addEvent(myInput,'click',function(){
            console.log('绑定第一个事件')
        })
        addEvent(myInput,'click',function(){
            console.log('绑定第二个事件')
        })
        addEvent('myInput','click',function(){
            console.log('绑定第三个事件')
        })

 "如此一来，在团队开发中就能安心的为元素绑定事件了" 小白感叹道
 
 #### 除此之外

"不过你之前写的代码问题不止这一个，之前说了，外观模式可以简化底层接口复杂性，也可以解决浏览器兼容性问题，而你前面写的代码除了绑定事件问题外，另外两处问题是在其他IE低版本浏览器中不兼容e.preventDefault()和e.target你也可以通过外观模式来解决"       

        //获取事件对象
        var getEvent = function(event){
            //标准浏览器返回event,IE下window.event
            return event || window.event
        }
        //获取元素
        var getTarget = function(event){
            var event = getEvent(event);
            //标准浏览器下event.target,IE下event.srcElement
            return event.target || event.srcElement;
        }
        //阻止默认行为
        var preventDefault = function(event){
            var event = getEvent(event);
            //标准浏览器
            if(event.preventDefault){
                event.preventDefault();
            }else{
                event.returnValue = false;
            }
        }

"有了上面的方法我们就可以用兼容的简单方式来解决上面的问题了"

        document.onclick = function(e){
            //阻止默认行为
            preventDefault(e);
            //获取事件源目标对象
            if(getTarget(e) !== document.getElementById('myInput')){
                hideInputSug();
            }
        }

#### 小型代码库

"小白，外观模式可以将浏览器不兼容的方法变得简单而又兼容各个浏览器，然而这只是外观模式应用的一部分，很多代码库中都是通过外观模式来封装多个功能，简化底层操作方法，比如我们简单实现获取元素的属性样式的简单方法库"

        var A  = {
            //通过ID获取元素
            g : function(id){
                return document.getElementById(id);
            },
            //设置元素css属性
            css:function(id,key,value){
                document.getElementById(id).style[key] = value;
            },
            //设置元素的属性
            attr:function(id,key,value){
                document.getElementById(id)[key] = value;
            },
            html:function(id,html){
                document.getElementById(id).innerHTML = html;
            },
            //为元素绑定事件
            on:function(id,type,fn){
                document.getElementById(id)['on' + type ] = fn;
            }
        }


"通过这个代码库，我们再操作元素的属性样式时变得更简单"

        A.css('box','background','red')//设置css样式
        A.attr('box','className','box')//设置class
        A.html('box','这是新添加的内容')//设置内容
        A.on('box','click',function(){//绑定事件
            A.css('box','width','500px');
        })

#### 忆之获

当一个复杂的系统提供一系列复杂的接口方法时，为系统的管理方便会造成接口方法的使用极其复杂，这在团队的多人开发中，撰写成本是很大的，当然通过外观模式，对接口的二次封装隐藏其复杂性，并简化其使用是一种很不错的实践，当然这种实践增加了一些资源开销以及程序的复杂度，当然这种开销相对于使用成本来说有时也是可忽略的。

外观模式是对接口方法的外层封装，以供上层代码调用，因此有时外观模式封装的接口方法不需要接口的具体实现，值需要按照接口使用规则使用即可，这也是对系统与客户(使用者)之间的一种松散耦合，使得系统与客户之间不会因结构的变化而相互影响


****

#### 适配器模式

适配器模式(Adaper):将一个类(对象)的接口(方法或者属性) 转化成另外一个接口，以满足用户需求，使类(对象)之间接口的不兼容问题通过适配器得以解决

随着活动页面的功能增加，原生Javascript在一些交互与特效实现上让小白感到力不从心，于是想引入大名鼎鼎的jQuery

#### 引入jQuery

"小白，咱们的作品活动页面还在用我们公司内部开发的A矿建，可是很多新来的同事使用A矿建开发新的功能需求时总是感觉很吃力，而且能用的方法有限，为了让他们尽快融入项目的开发， 我想让你引入jquery框架没问题吧" 小明对小白说

"没问题，" 小白看了一眼代码，迟疑一下 "可是以前功能缩写的代码是不是我还要重新用jquery写一遍，比如像这里引入的事件"

        A(function(){
            A('button').on('click',function(e){
                //.....
                })
            })


"不用啊，咱么公司的A框架与jquery框架比较像，所以你简单写个适配器就可以了"

"适配器，" 小白不解，"那是什么东西"

#### 生活中的适配器

"以前你没有接触过么？" 小明接着说"这可是编程中一种常见的模式，其实生活中这种模式也很常见，你看公司的睡房的两根垂直相交的水管连接处的直角弯管了么？它就是一个适配器，它是的两个不同方向的水管可以疏通流水，再比如我们三角插头手机充电器对于两项插头是不能用的，此时我们就需要一个三项转两项插头电源适配器等等，这些都是适配器，如果你明白这些，那么为页面中的代码写适配器就不难了，其实就是为两个代码库缩写代码兼容运行而书写的额外代码，有了这样的适配器，你就不需要特意的重写以前的功能代码了，你只需要让用以前的代码库缩写的代码适配jquery就可以了"

"可是我改如何做呢?" 小白追问

#### jquery适配器

"你看我们公司的A框架代码书写格式是不是与Jquery代码书写格式很想，所以你需要在加载完jquery框架后写一个适配器，将我们已有的功能适配到jquery，比如代码中有两个事件，一个页面加载事件，一个点击事件，不过这两个事件与Jquery中的写法很像，所以这里就不用做多少改动了，我们的适配器主要的任务是适配两种代码库中不兼容的代码，那么首当其冲的就是全局对象A与jquery了，所以你可以像下面这样轻松实现"

>window.A = A = jquery

"小白，你刷新页面看看是不是运行良好" 小明笑着问

小白刷新了一下页面"真是太神奇了，页面可以正常工作了，这样我们就可以写以前熟悉的jquery了"

#### 适配异类框架

"恩，这是因为咱么公司的整个轻量级的A框架太像jquery了，我们可以将两种框架看成是相似框架，但是如果一个框架与jquery血缘远一点，那么对于这种异类框架适配情况就复杂得多了，举个例子吧，还是实现上面两个事件，所以我写了一个这样的框架"


        var A = A || {};

        //通过ID获取元素
        A.g = function(id){
            return document.getElementById(id);
        }
        //为元素绑定事件
        A.on = function(id,type,fn){
            //如果传递参数是字符串则以ID处理，否则以元素对象处理
            var dom = typeof id === 'string' ? this.g(id) : id;
            //标准DOM2级添加时间方式
            if(dom.addEventListener){
                dom.addEventListener(type,fn,false);
            }else{
                //IE 标准DOM2级添加事件方式
                dom.attachEvent('on' + type,fn);
            }else{
                dom['on' + type ] = fn;
            }
        }

"那么要完成上面的需求我们可以这样做"

        //窗口加载完成事件
        A.on('window','load',function(){
            //按钮点击事件
            A.on('mybutton','click',function(){
                //do something    
            })
        })

"好了，小白，那么我想引入jquery来还原有的ID苦，你只该如何做么？"

小白思考了以下说:"首先g方法是通过ID获取元素，所以通过$(jquery的简写名称)方法获取jquery对象然后通过get获取第一个成员即可，不过on方法有些复杂，我们不能直接替换，因为jquery和我们A库在通过ID获取元素时时有区别的，jquery的ID前面要加#所以异类矿建的适配器应该是这样的吧"


        A.g = function(id){
            return $(id).get(0);//通过jquery获取jquery对象，然后返回第一个成员
        }
        A.on = function(id,type,fn){
            //如果传递参数是字符串则以ID处理，否则以元素对象处理
            var dom = typeof id === 'string' ? $('#'+id):$(id);
            dom.on(type,fn);
        }

"你还是很聪明的，是这样，通过适配器我们发现如果两种框架的'血缘'比较相近，那么我们适配起来是比较容易的，如果'血缘'相差甚远我们的适配器写起来要复杂的多，因此你要记住，日后飞到万不得已请情况下，尽量引入相似框架"

"是啊，后一种要写不少代码啊" 小白补充说

#### 参数适配器

"除此之外，适配器还有很多用途，比如方法需要传递多个参数，例如..."

>function doSomething(name,title,age,color,size,prize){}

"那么我们记住这些参数的顺序是很困难的，所以我们经常是以一个参数对象方式传入的"

        /**
         * obj.name:name
         *obj.title:title
         *obj.age:age
         *obj.color:color
         *obj.size:size
         *obj.prize:prize
         */

>function doSomething(obj){}

"然而当调用它的时候又不知道传递的参数是否完成，如有一些参数没有传入，一些参数是有默认值的等等，此时我们通常的做法就是用适配器来适配传入的这个参数对象，如下所示"

        function doSomething(obj){
            var _adapter = {
                name:"雨夜清荷",
                title:"设计模式",
                age:24,
                color:"pink",
                size:100,
                prize:50
            };
            for(var i in _adapter){
                _adapter[i] = obj[i] || _adapter[i];
            }
            //或者extend(_adapter,obj) 注此时可能会多添加属性
            //do things
        }


#### 数据适配

"没看出你接触过插件开发" 小明接着说"对于这类对参数的适配又有衍生，比如数据的适配，比如这有一个数组"

>var arr = ['Javascript,'book','前端编程语言','8月1日'];

"我们发现数组中的每个成员代表的意义不同，所以这种数据结构语义不好，我们通常将其适配成对象格式，比如下面这种对象数据结构"

>var obj = {
>       name:"",
>       type:"",
>       title:"",
>       time:""
>    
>}

"我们就可以像下面这样适配"
        
        function arrToObjAdapter(arr){
            return {
                name:arr[0],
                type:arr[1],
                title:arr[2],
                data:arr[3]
            }
        }

        var adapterData = arrToObjAdapter(arr);
        console.log(adapterData) //{name:"javascript",type:"book",title:"前端编程语言",data:"8月1日"}

"这也为数据的灵活使用提供了新思路了" 小白感叹道

#### 服务器端数据适配

"是啊" 小明接着说"但是，你知道么， 最重要的是它解决了前后端的数据依赖，前端程序不再为后端传递的数据所束缚，如果后端因为架构改变导致传递的数据结构发生变化，我们只需要写个适配器就可以放心了，比如我们用jquery想后端someAdress.php接口请求数据，然后用dosomething方法处理接收的格式，我们在调用dosomething方法时最好不哟啊直接调用，最好先将传递过来的数据适配成对我们可有的数据在使用，这样将更安全，如下面的例子"

        //为简化模型，这里使用Jquery的Ajax方法，理想数据是一个一维数组
        function ajaxAdapter(data){
            //处理数据并返回新数据
            return [data['key1'],data['key2'],data['key3']];
        }
        $.ajax({
            url:'something.php',
            success:function(data,status){
                if(data){
                    //使用适配后的数据--- 返回的对象
                    doSomething(ajaxAdapter(data))
                }
            }
        });

"像这样。如果日后后端数据有任何变化我们只需响应的更改ajaxAdapter适配器转化格式就可以了"


### 忆之获

传荣设计模式中，适配器模式往往是适配两个接口不尖肉的问题，然而在javascript中，适配器的应用范围更广，比如适配两个代码库， 适配前后端数据，等等

Javascript中的适配器的应用，更多应用在对象之间，为了使对象可用，通常我们会将对象 差费并重新包装，这样我们就要了解适配对象的内部结构，这也是与外观模式的区别所在，当然适配器模式同样解决了对象之间的耦合度，包装的适配器代码增加了一些资源开销，当然这是微乎其微的。


--------

#### 代理模式


代理模式(proxy):由于一个对象不能直接饮用另一个对象，所以需要通过代理对象在这两个对象之间起到中介的作用

由于用户相册模块上传的照片量越来越大，导致服务器端需要将图片上传模块重新部署到另外一个域(可理解为另一台服务器)中，这样对于前端来说，用户上传图片的请求路径发生变化，指向其他服务器，这就导致跨域问题


#### 无法获取图片上传模块数据

"小名 你帮我看看，为什么我向咱们图片上传模块所在的服务器发送的请求，得不到数据呢？" 小白问小明道

        //当前域www.xx.com
        $.ajax({
            url:http;//upload.xx.com/upload.php,
            success:function(res){
                //无法获取返回的数据
            }    
        })

"打开你的控制台，你发现没有，已经报错了，出现蛞蝓问题了"

>//浏览器控制台报错，XMLHttprequest cannot load http://upload.xx.com/upload.php no 'Access-Control-Allow-Origin' header is present on the requested resource

#### 一切只因跨域

"哦，为什么会出现，什么是跨域?" 小白问

"由于javascript对安全访问因素的考虑，不允许跨域调用其他页面，这里的域你可以想象成域名，比如百度的域名http://www.baidu.com，淘宝的域名http://www.taobao.com，不同域名下的页面是不能直接调用的，这样百度域名加的页面是不允许直接调用淘宝页面的，这也是一种javascript中因同源策略所定义的限制，不过仅此一点限制还不够，javascript还对同一域名不同的端口号，同一玉面不同协议，域名和域名对应的IP，主域与子域、子域与子域等做了限制，都不能直接调用，如下所示"

同一域名不同的端口号:http://www.baidu.com:8081与http://www.baidu.com:8002
同一域名不同协议:http://www.bai.com与https://www.baidu.com
域名和域名对应的IP:http://www.baidu.com与http://61.135.169.125
主域与子域:http://www.baidu.com与http://b.a.com
子域与子域:http://tieba.baidu.com与http://fanyi.baidu.com

"这么多限制，原来我刚才遇到的情况是正是主域与子域之间的跨域造成的啊，那么总是这样，在主域下，我的相册页面还能与子域中的图片上传模块所在的服务器之间进行通信么？"

"这就需要一些技巧了，你看，相册页面与图片上传模块所在的服务器之间你可抽象成两个对象，那么现在的问题是，他们之间被一条河隔开了，就像天河两端的牛郎织女，只能远远观望而不能相聚一键，他们的情感感动万物，所以才有那么多需求为他们搭桥，同样你想让跨域两端的对象之间实现通信，你就需要找个代理对象来实现他们之间的通信"

"我明白了，虽然他们之间分开了，但是我们可以找一个代理对象来实现相互之间的通信，不过对于这类代理对象又有哪些呢?" 小白问小明道

#### 站长统计

"当然，代理对象有很多，简单一点的如img之类的标签通过src属性可以像其他域下的服务器发送请求，不过这类请求是get请求，并且是单向的， 他不会有响应数据，就好比你站在河的一遍向另一边发消息，却又不想让别人听见，所以你可以将你的消息写在纸上放在口袋里，然后扔过去，不过河对岸有没有人接收到你的消息就不得而知了"

"你说的还挺有意思的，不过这类代理对象有什么应用啊" 小白问

"很多啊，比如一些站长平台会有对于你的页面的统计项，其实现原理就是在你的页面触发一些动作的时候向站长平台发送这类img的get请求，然后他们会对你发的请求做统计，然而你并不知道统计的相关消息" 小明解释道

        //统计代理
        var Count = (function(){
            //缓存图片，
            var img = new Image();
            return function(param){
                //统计请求字符串
                var str = 'http://www.count.com/a.gif';
                //拼接请求字符串
                for(var i in param){
                    str += i + '=' + param[i];
                }
                //发送统计请求
                img.src= str;
            }
            })()
            //测试用例，统计num
            Count(num:10);


#### JSONP

"第二种代理对象形式就是通过script标签，比如我们在CDN(内容分发网络，一种更接近用户的网络架构，是用户可以就近获取内容)上更快速的获取jquery文件时，用script来获取，然而这种获取方式获取的script内容是不变的，而我们需要的代理对象，是对页面与浏览器间痛下的，显然上面的方式还不能满足我们的需求，不过我们知道通过src属性可实现get请求，因此我们可以在src指向的url(请求地址)上面添加一些字段信息，然后服务器端获取这些字段，再响应的生成一份内容"

        //前端浏览器页面
        <script type="text/javascript">
        //回调函数，打印出请求数据与响应数据
        function jsonpCallBack(res,req){
            console.log(res,req);
        }
        </script>
        <script type="text/javascript" src="http://localhost/test/jsonp.php?callback=jsonp CallBack&data=getJsonPData"></script>
        //另外一个域下服务器请求接口
        <?php
        //后端获取请求字段数据，并生成返回内容
        $data = $_GET['data'];
        $callback = $_GET['callback'];
        echo $callback."('success','".$data."')"

这种方式，你可以想象成合理面的一只小船，通过小船将你的请求发送给对岸，然后对岸的人们将数据放在小船里为你带回来

"哦，那这种方式就需要其他域下的服务器端与前端协同工作开发功能了吧"

#### 代理模板

"当然，这种方式还要求其他域要有一定可靠性，否则将会攻击到你的网站，当然这种方式也被人称之为JSONP方案，有时我们还会通过一个方法来动态生成需要的JSONP中script标签，与之类似的还有一种方案是被称之为代理模板的方案，他的解决思路是这样的，既然不同域之间相互调用对方的页面是有限制的，那么子集域中的两个页面相互之间的调用是可以的，即代理页面B调用被代理的页面A中对象的方式是可以的，那么要实现这种方式我们只需要在被访问的域中，请求返回Header重定向到代理页面，并在代理页面中处理被代理的页面A就可以了"

"既然这样，是不是我们在自己的域中药有这样A。B两个页面了" 小白问

"是的，比如我们将自己的域成为X域，另外的域成为Y域X域中要有一个呗dialing页面即A页面，在A页面中应该具备三个部分，第一个部分是发送请求的模块，如form表单提交，负责向Y域发送请求，并提供额外两组数据，其一是要执行的回调函数名称，其二是X域中代理模板所在的路径，并将target目标指向内嵌框架，第二个部分是一个内嵌框架，如iframe负责提供第一个部分中form表单的响应目标targe的指向，并将嵌入X域中的代理页面作为子页面，即B页面，第三个部分是一个回调函数，负责处理返回的数据"

X域中被代理页面A

        <script type="text/javascript">
            function callback(data){
                console.log('成功接收数据',data);
            }
        </script>
        <iframe name="proxyIframe" id="proxyIframe" src="">

        </iframe>

        <form action="http://localhost/test/proxy.php" method ="post" target="proxyIframe">
            <input type="text" name="callback" value="callback" placeholder="">
            <input type="text" name="proxy" value="http://localhost:8080/proxy.html" placeholder="">
            <input type="submit" name="" value="提交" placeholder="">
        </form>

"其次在X域中我们也要有一个代理页面，主要负责将自己页面URL中searcher部分的数据解析出来，如http://www.a.com?type=1&title=aa这个URL中searcher部分指的是就是?type=1&title=aa 将数据重新组装好，调用A页面里的回调函数，将组装好的数据作为参数传入父页面中定义的花掉函数中并执行"

X域中代理页面B

        
        <script type="text/javascript">
            //页面加载后执行

            window.onload = function(){
                //如果不在A页面中返回，不执行
                if(top == self) return 
                //获取并解析searcher中的数据
                var arr = location.search.substr(1).split('&'),
                //预定义函数名称以及参数集
                fn,args;
                for(var i = 0; i < arr.length; i ++){
                    //解析searcher中的魅族数据
                    item = arr[i].split('=');
                    //判断是否为回调函数
                    if(item[0] =='callback'){
                        /设置回调函数
                        fn = item[i];

                        //判断是否是参数集

                    }else if(item[0] == 'arg'){
                        //设置参数集
                        args =item[1];
                    }
                }
                try{
                    //执行A页面中预设的回调函数
                    eval('top' + fn + '("' + args + '")');
                }catch (e){

                }
            }
        </script>

"最后是Y域中的呗请求的接口文件C，它的主要工作室将从X域过来的请求，数据解析并获取回调函数字段与代理模板路径字段数据，并打包返回，并将自己的Header重定向为X域的代理模板B所在路径"

            <?php 
            $proxy = $_POST['proxy'];
            $callback = $_POST['callback'];
            header("Location: " .$proxy.?callback=".$callback." & arg=success);?>

测试结果
        
            /*控制台输出依次是，成功接收数据success*/ 

### 忆之获

通过集中dialing模式对跨域问题的解决方案，我们可以看到代理对象可以完全解决被代理对象与外界对象之间的耦合，当然从对被代理的页面角度来看是一种抱回代理，然而从服务器角度来看有事一种远程代理，除了在跨域问题中有很多应用中，有时对对象的实例化对资源的开销很大，如页面加载初期加载文件有很多，此时能够延迟加载一些图片对页面首屏加载时间收益是很大的，再比如图片预览页面，页面中有很多图片，面对这么多的图片如果一一加载对资源的开销也是很可怕的，所以通常是当用户点击某张图片时加载这张图片，但如果该图片源文件也很大，此时我们通常的做法是先代理加载一张预览图片，然后再讲原图片替换这张预览图片，这种代理有时也成为虚拟代理

由此可见代理模式可以解决系统之间的耦合度以及系统资源开销大的问题，通过代理对象可保护被代理对象，使被代理对象拓展性不受外界的影响，也可通过代理对象解决某一交互或者某一需求中造成大量系统开销

当然无论代理模式在处理系统。对象之间的耦合度问题还是在结局系统资源开销问题，他都讲构建出一个复杂的代理对象，增加系统的复杂度，同事也增加了一定的系统开销，当然有时对于这种开销往往是可接受的

在Javascript中，它的执行常常依托于浏览器，所以代理模式解决问题的思想有事也为我们提供了一些解决问题的方案。

--------

#### 装饰者模式

装饰者模式(Decorator):在不改变元对象的基础上， 通过对其进行包装拓展(添加属性或者方法)使原有对象可以满足用户的更复杂需求

静止是相对的，运动是绝对的，所以没有一成不变的需求，这不，为增强用户使用表单的交互体验，项目经理找来小白，正在谈后续需求改进呢

"小白"，项目经理走过来，"用户信息表单需求有些变化，以前是当用户点击输入框时，如果输入框输入的内容有限制，那么气后面显示用户输入内容的限制格式的提示文案，现在我们要多加一条，默认输入框上边显示一行提示文案，当用户点击输入框时文案消失"

小白一听心想:"这很简单，找到对应的代码，然后在后面增加几句就可以了嘛"，于是小白浏览一下前任写过的代码。

    //输入框元素
    var telInput = document.getElementById('tel_input');
    //输入格式提示文案
    var telWranText = document.getElementById('tel_wran_text');
    //点击输入框显示输入框输入格式提示文案
    input.onclick = function(){
        telWranText.style.display = 'inline-block';
    }
    //于是小白不假思索的修改了这些写过的代码
    //输入框元素
    var telInput = document.getElementById('tel_input');
    //输入框输入格式提示文案
    var telWranText = document.getElementById('tel_warn_text');
    //点击输入框显示输入框输入格式提示文案并隐藏输入提示文案
    input.onclick = function(){
        telWranText.style.display = 'inline-block';
        telDemoText.style.display = 'none';
    }

可是悲剧发生了，小白修改了一个电话输入框，后面还有姓名输入框，地址输入框，等等，还要像电话输入框这样在文件中查找功能代码，然后一个一个修改么？ 小白皱起眉头。

小明看到后，走过来:"小白，怎么了"

项目经理让我给原来用户信息输入框增加一些需求，然而我改一个容易，后面还有这么多输入框，我还要一个一个去文件中查找代码，真不知道该如何是好了

"哦，这样啊，试试装饰者模式吧"

"装饰者模式，以前没有听过，是添加东西的意思么"

#### 装饰已有的功能对象

"恩，很简单，比如你买一个房子，你想住的更舒适，那么你刚刚买的为装饰过的新房子就不能满足你的需求了，所以你要对其装修一番，放置一个床，摆上一个沙发，抬进来一个电视，这样生活更舒适，同样，装饰者模式也是这个道理，原有的功能已经不能满足用户的需求了，此时你要做的就是为原有功能添砖加瓦，设置新功能和属性来满足用户提出的需求，"

"我明白一些了，不过我要如何实现呢？"

"首先明确原有的功能是那些，看看你已经写过的功能代码，这些就是原有的功能，你要做的就是在这基础上添加一些功能来满足用户提出的需求"

    //装饰者
    var decorator = function(input,fn){
        //获取事件源目标对象
        var input = document.getElementById(input);
        //若时间源已经绑定事件
        if(typeof input.onclick ==='function'){
            //缓存时间源原有回调函数
            var oldClick = input.onclick;
            //为事件源定义新的事件
            input.onclick = function(){
                //事件源原有回调函数
                oldClick();
                //执行事件源新增回调函数
                fn();
            }
        }else{
            //事件源为绑定事件，直接为事件源添加新增回调函数
            input.onclick = fn;
        }
        //做其他事情
    }

#### 为输入框添砖加瓦

"看看上面的代码，此时装饰者不仅仅可以对绑定过事件的输入框添加新的功能，未绑定过的输入框同样可以，你可以像下面这样调用" 

    //电话输入框功能装饰
    decorator('tel_input',function(){
        document.getElementById('tel_demo_text').style.display = 'none';    
    })
    //姓名输入框功能装饰
    decorator('name_input',function(){
        document.getElementById('name_demo_text').style.display = "none";    
    });
    //地址输入框功能装饰
    decorator('adress_input',function(){
        docuemnt.getElementById('address_demo_text').style.display = "none";    
    });

"真是太棒了，通过使用装饰者对象方法，无论输入框是否绑定过事件，都可以轻松完成增加隐藏示例框的需求，真的很不错，" 小白感叹道

"装饰者模式很简单，就是对原有对象的属性与方法的添加"

小白想了想问:"前几天我们学过的适配器模式也是对一个对象的装饰来适配其他对象，那么它与装饰者模式有什么不同呢？"

"适配器方法是对原有对象适配，添加的方法与原有方法功能上大致相似，但是装饰者提供的方法与原来的方法功能项是有一定区别的，不需要了解对象原有的功能，并且对象原有的方法照样可以原封不动的使用，"小明答道

"哦，对了，你也提醒了我，这么说既然在适配器模式中增加的方法要调用原有方法，是不是就要了解原有方法实现的具体细节，而在装饰者中原封不懂的使用，我们就不需要知道原有方法实现的具体细节，只有当我们调用方法时才会知道的"

"恩，正式这样" 小明笑了

### 忆之获

通过小白对输入框交互功能的拓展，我们学习了一种可以在不了解原有功能的基础上对功能拓展模式，这是对原有功能的一种增强与拓展，当然同样对原有对象进行拓展的模式还有适配器模式，所不同的是适配器进行拓展很多时候是对对象内部结构的重组，因此了解其自身结构是必须的，而装饰者对对象的拓展是一种良性拓展，不用了解其具体实现，只是在外部进行了一次封装拓展，这又是对原有功能完整性的一种保护

--------

#### 桥接模式

桥接模式(Bridge):在系统沿着多个维度变化的同事，又不增加其复杂度并已达到解耦。有时候页面中的一些小小细节改变常常因逻辑相似导致大片臃肿的代码，让页面苦涩不堪，小白为解决这类问题，已经熬了整整一上午了

#### 添加事件交互

"小白，什么功能让你谢了一上午" 小明问道

"这不，项目经理让我把页面上不的用户信息部分添加一些鼠标划过特效"

小白接着说:"哎，不过用户信息有很多小部件组成，你看，对于用户名，鼠标划过直接改变背景色，但是像用户等级，用户信息这类不见只能改变里边的数字内容，处理的逻辑不太一样，所以写了不少代码，不过写完时，自己柑橘很多是陈宇的，却又不知道该如何改善"

"哦，来让我看看你的代码吧"

    var spans = document.getElementsByTagName('span');
    //为用户绑定特效
    spans[0].onmouseover = function(){
        this.style.color = 'red';
        this.style.background= '#ddd';
    }
    spans[0].onmouseout = function(){
        this.style.color = '#333';
        this.style.background = '#f5f5f5';
    }

    //为等级绑定特效

    spans[1].onmouseover =function(){
        this.getElementsByTagName('strong')[0].style.color = 'red';
        this.getElementsByTagName('strong')[0].style.background="#ddd";
    }
    spans[1].onmouseout = function(){
        this.getElementsByTagName('strong')[0].style.color='#333;
        this.getElementsByTagName('strong')[0].style.background="#f5f5f5";
    }

### 提取共同点

"看你的代码是有点，不过你知道你的问题在那里么？"

"要对事件的回调函数再做处理么?" 小白问小明道

"恩，你在写代码时一定要注意对相同的逻辑做抽象提取处理，这一点很重要，如果这一点你能做到，那么你的代码将会更加简洁，重用率也会更大，当然可读性更高，这也是我推荐你使用面向对象思想编程的一个目的" 小明接着说:"对于用户信息模块的每一个部分鼠标划过与鼠标离开两个事件的执行函数由很大一部分是相似的，比如他们都处理每个部件中的某个元素，他们都是处理改元的字体颜色和背景颜色，所以对于这个相似点的抽象提取是很有必要的，因此你可以创建下面这样一个函数，让它解除与事件中的this的耦合"

    //抽象
    function changeColor(dom,color,bg){
        //设置元素的字体颜色
        dom.style.color = color;
        dom.style.background = bg;
    }

#### 事件与业务逻辑之间的桥梁

"剩下你要做的就是对元素进行绑定事件了，但是有一点你要明白，仅仅知道元素事件绑定与抽象提起的设置样式方法changeColor还是不够的，你需要用一个方法将它们链接起来，那么这个方法就是桥接方法，这种模式就是桥接魔爱黑丝，就像你在北京开着车去沈阳旅游，那么你就要找到一条连接北京与沈阳的公路，才能顺利的两地王法"，小明接着说:"那么对于事件的桥接方法，我们可以用一个匿名函数代替，否则直接将changeColor作为事件的回调函数，那么我们刚才所作的事情就白做了，因为它们还将耦合在一起，如下面的用户绑定事件"    

    var spans = document.getElemensByTagName('span');
    spans[0].onmouseover = function(){
        changeColor(this,'red','#ddd');
    }

"changeColor方法中的dom实质上是事件回调函数汇总的this,那么我们想接触它们之间的耦合，我们就需要一个桥接方法---匿名回调函数，通过这个回调函数我们将获取到的this传递到changeColor函数中，即可实现需求，同样对于用户名模块的鼠标一开事件用同样的方式即可"  

    spans[0].onmouseout = function(){
        changeColor(this,'#333','#f5f5f5');
    }

"好了，小白，对于用户等级这类特殊的需求你知道该怎么做了吧" 小明道

"恩，既然用户名模块的this在桥接匿名函数中获取，那么也应该是同样的道理应用在用户等级上，通过桥接函数来获取数字元素，然后闯入changColor就可以了吧，"

    spans[1].onmouseover = function(){
        changeColor(this.getElementsByTagName('strong')[0],'red','#ddd');
    }
    spans[1].onmouseout = function(){
        changeColor(this.getElementsByTagName('strong')[0],'#333','#f5f5f5');
    }

"恩，小白你再来看看是不是现在与之前相比清晰多了，如果再想对需求做任何修改我们只需要修改changeColor的内容就可以了，而不比取到每个时间回到函数中去修改，当然这种实现方法看起来调理更清晰，但是别忘了她是以新增一个桥接函数为代价实现的"

"是啊， 听你说的，感觉桥接模式只是先抽象提取共用部分，然后将实现与抽象通过桥接方法链接在一起，来实现解耦的作用的吧"

#### 多元化对象

"你所得对，不过桥接模式的强大之处不仅仅在此，甚至对于多维的变化也同样适用，比如我们书写一个canvas跑步游戏的时候，对于游戏中的人、小精灵、小球等一系列的实物都有动作单元，而他们的每个动作实现起来方式又都是统一的，比如人和精灵和求的运动其实就是位置坐标X和Y的变化，求的颜色与精灵的色彩的绘制方式都相似等，这样我们可以将这些多维变化部分，提取出来作为一个抽象运动单元进行保存，而当我们创建实体时，将需要的每个抽象动作单元通过桥接，链接在一起运作，这样它们之间不会相互影响并且该方式降低了它们之间的耦合。"

    //多维变量类
    //运动单元
    function Speed(x,y){
        this.x = x ;
        this.y = y ;

    }
    Speed.prototype.run = function(){
        console.log('跑起来')
    }
    //着色单元
    function Color(cl){
        this.color = cl;
    }
    Color.prototype.draw = function(){
        console.log('绘制色彩')
    }
    //变形单元
    function Shape(sp){
        this.shape = sp;
    }

    Shape.prototype.change = function(){
        console.log('改变形状')
    }
    //说话单元
    function Speek(wd){
        this.word = wd;
    }
    Speek.prototype.say = function(){
        console.log('书写字体');
    }

"于是我们想创建一个类，并且它可以运动，可以着色"

    function Ball(x,y,c){
        //实现运动单元
        this.speed - new Speed(x,y);
        //实现着色单元
        this.color = new Color(c);
    }
    Ball.prototype.init = function(){
        //实现运动
        this.speed.run();
        //实现着色
        this.color.draw()
    }

"同样我们想创建一个人物类，他可以运动以及说话"

    function People(x,y,f){
        this.speed = new Speed(x,y);
        this.font = new Speek(f);
    };

    People.prototype.init = function(){
        this.speed.run();
        this.font.say();
    }

"当然我们也可以创建一个精灵类，让它可以运动可以着色可以改变形状"

    function Spirite(x,y,c,s){
        this.speed = new Speed(x,y);
        this.color = new Color(c);
        this.shape = new Shape(s);
    };

    Spirite.prototype.init = function(){
        this.speed.run();
        this.color.draw();
        this.shape.chagne();
    }

"当我们想实现一个任务时，我们直接实例化一个人物对象，这样他就可以有运动和说话的动作了"

    var p = new People(10,12,16);
    p.init();

### 忆之获

桥接模式最主要的特点既是将实现层(如元素绑定的时间)与抽象层(如装饰页面UI逻辑)解耦分离，使两部分可以独立变化，由此可以看出桥接模式主要是对结构之间的结构，而前面学过的抽象工厂模式与创建者模式主要业务在于创建，通过桥接模式实现的解耦，使实现层与抽象层分开处理，避免需求的改变造成对象内部的修改，提现了面向对象对拓展的开发及对修改的关闭原则，这是很有用的。

当然由于桥接的添加，有时也造成开发成本的增加，有时性能上也会受到影响。
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




