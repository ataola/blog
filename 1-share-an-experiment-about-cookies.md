# Share an experiment about cookies

> The experiment itself is very boring, I try to make it interesting.

## Cause

I went to the Internet to search for the introduction of cookies, and I read several articles that looked very similar. I castrated the content and said that "different browsers limit the number of cookies differently, roughly in the range of 30-50, (prefix) browser Allow Cookie up to about 4KB, including name, value, equal sign".

First, the information I read is not particularly authoritative, and they are all blog posts on the Internet. I have a question about the browser limit of 30-50. Is it true? The second is to allow up to about 4KB, which is very confusing. Whether the total value of all cookies under a domain name is about 4KB, or the information represented by a Name of a single cookie can be about 4KB, which makes I'm so lost.

Okay, then let's do an experiment about cookies to verify some things.

* What is the maximum number of browser cookies under a single domain name?
* How big can a single value of a browser cookie be?

## After

### modeling

Before starting the experiment, let's build a model, roughly how the experiment will unfold, as shown in the figure above.

![img](https://img2020.cnblogs.com/blog/2055171/202008/2055171-20200824104815743-1679313125.png)

At first, I provided a manual transmission model. You can try to enter the name and value, and then click the button Add Cookie, it will write this record into the cookie. In order to facilitate comparison, I read the information of the cookie Synchronized a copy to the webpage, so it looks more intuitive. Since we want to record the number of cookies, here the author simply and rudely sets it in the upper right corner of the visible content of the web page, the red place. Later, I wanted to be a little lazy, so he implemented a manual block model Add Random Cookie that randomly generates cookies. All subsequent experimental results are also based on this basis.

After writing the program, I first tested it in the latest version of Chrome browser. The rule found is that when the number of cookies reaches 180, it will drop to 150 if it is increased, which means that 180 is its upper limit, and it will automatically clear 30 players after that.

![img](https://img2020.cnblogs.com/blog/2055171/202008/2055171-20200824104835142-1734962356.gif)

The problem here is that the author randomly stuffed it twice on the name and value respectively. Through observation, it is difficult for us to find out how it deletes after reaching the upper limit. Is it to delete the first 30, the last 30, or randomly?

Okay, let's change it, our naked eyes are more sensitive to numbers, so let's replace all its values with numbers to see.

![img](https://img2020.cnblogs.com/blog/2055171/202008/2055171-20200824104902917-878200537.png)

You can see that it deleted the first 30 cookie records.

In my mobile phone, the result of opening Xiaomi's built-in browser is the same as this.

Next, let's test the situation in the Firefox browser. The version of the Firefox browser on the author's computer is still relatively low, and it has not been upgraded to the latest version. Because the 48.0.2 version can directly install some xpi plug-ins manually, the author is here This version has firebug and other plugins installed.

![img](https://img2020.cnblogs.com/blog/2055171/202008/2055171-20200824104918307-1398044160.gif)

Through observation, we can see that in the Firefox browser, its rule is that when the number of cookies reaches 150, it will delete the first cookie and leave a new cookie in the vacant position. Its upper limit is 150, if you add another cookie record later, you will delete the first cookie record to make room for the later addition.

At this point, the author organizes the relevant cookie information into files. The result of two random cookies is about 6KB, and the result of adding Arabic to one random cookie is about 3KB. Seeing this, we can guess that the 4KB limit mentioned at the beginning should refer to a record set by Cookie.

Of course, we study science very rigorously, let's see the results through experiments.

![img](https://img2020.cnblogs.com/blog/2055171/202008/2055171-20200824104944634-1135320613.png)

The author wrote a test program. After testing, it was found under the conditions of the Chrome browser that it was about 4KB.

## Result

Under certain conditions, the browser based on the Webkit kernel, the cookies show the following rules. When the number of cookies under a single domain name reaches 180, adding it again will delete the first 30 cookies, and then start from the base of 150. After increasing to 180, the browser will cycle the previous operations.

Under certain conditions, the browser based on the gecko kernel has the following rules for cookies. When the number of cookies under a single domain name reaches 150, adding it again will delete the first cookie record to make room for the added cookie record.

Under certain conditions, the value of a single cookie record is allowed to be approximately 4KB in size.

## Finally

Finally, attach the address related to the experiment: https://zhengjiangtao.cn/show/zj/cookie.html

I come from a beautiful country called China, I like to see the world and make friends, if you have a remote front-end job to offer, I'm glad to work for you, thank you!