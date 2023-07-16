---
layout: documentation-vuejs
title:    props
cattitle:   اصول آموزش vuejs
date:   2021-05-14 17:02:42 +0330
jdate: جمعه 24 اردیبهشت 1400
caturl: 2019/10/11/vuejs.html
#  permalink: /:categories/:title.html
directory : vuejs/Components-In-Depth
menu : false
thumbnail: vuejs.jpg
refrence: https://vuejs.org/v2/guide/components-registration.html
---
<p>
</p>


<h3 >Prop Casing (camelCase vs kebab-case)</h3>

<p>
نام ویژگی های HTML نسبت به حروف کوچک و بزرگ حساس نیستند ، بنابراین مرورگرها هر حرف بزرگ را به صورت کوچک تفسیر می کنند. این بدان معنی است که وقتی از الگوهای in-DOM  استفاده می کنید ، نام هایprop  که بصورت  camelCased  معرفی می شوند باید از معادل kebab-cased (جدا شده با خط فاصله) استفاده کنند.
</p>
<pre><code class="language-javascript  line-numbers">Vue.component('blog-post', {
  // camelCase in JavaScript
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
</code></pre>

<pre><code class="language-html  line-numbers">&#x3C;!-- kebab-case in HTML --&#x3E;
&#x3C;blog-post post-title=&#x22;hello!&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>
<p>
باز هم ، اگر از الگوهای رشته استفاده می کنید ، این محدودیت اعمال نمی شود.
</p>
<br>

<h3>  انواع Prop  (Prop Types)</h3>
<p>
تاکنون ، ما فقط لیست prop هایی را مشاهده کرده ایم که به عنوان آرایه ای از رشته ها لیست شده اند:
</p>

<pre><code class="language-javascript  line-numbers">props: ['title', 'likes', 'isPublished', 'commentIds', 'author']
</code></pre>

<p>
معمولاً ، شما می خواهید هر یک از prop  ها دارای نوع خاصی از مقدار  باشد. در این موارد ، شما می توانید لیست prop ها  را به عنوان یک object فهرست کنید:
</p>

<pre><code class="language-javascript  line-numbers">props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
</code></pre>

<p>
با اینکار نه تنها کامپوننت شما مستند می شود ، بلکه در صورت استفاده نوع اشتباه ، به کاربران در کنسول جاوا اسکریپت مرورگر نیز هشدار می دهد.  می توانید در مورد نوع بررسی و سایر اعتبار سنجی ها    <a href="https://vuejs.org/v2/guide/components-props.html#Prop-Validation" > type checks and other prop validations</a>اطلاعات بیشتری کسب کنید.
</p>

<br>

<h3> Passing Static or Dynamic Props</h3>
<p>
تاکنون مشاهده کرده اید که prop  ها  یک مقدار ثابت را عبور می دادند ، مانند:
</p>

<pre><code class="language-javascript  line-numbers">&#x3C;blog-post title=&#x22;My journey with Vue&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>

<p>
همچنین شما prop  هایی را دیده اید که با استفاده از v-bind  به صورت پویا ثبت شده اند ، مانند:
</p>

<pre><code class="language-html  line-numbers">&#x3C;!-- Dynamically assign the value of a variable --&#x3E;
&#x3C;blog-post v-bind:title=&#x22;post.title&#x22;&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Dynamically assign the value of a complex expression --&#x3E;
&#x3C;blog-post
  v-bind:title=&#x22;post.title + &#x27; by &#x27; + post.author.name&#x22;
&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>

<p>
در دو مثال بالا ، ما مقادیر رشته ای را منتقل کردیم ، اما هر نوع از مقدار می تواند به یک prop منتقل شود.
</p>

<br>
<h4>
<a href="#Passing-a-Number" class="headerlink" title="Passing a Number" data-scroll="">Passing a Number</a>
</h4>

<pre><code class="language-html  line-numbers">&#x3C;!-- Even though &#x60;42&#x60; is static, we need v-bind to tell Vue that --&#x3E;
&#x3C;!-- this is a JavaScript expression rather than a string.       --&#x3E;
&#x3C;blog-post v-bind:likes=&#x22;42&#x22;&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Dynamically assign to the value of a variable. --&#x3E;
&#x3C;blog-post v-bind:likes=&#x22;post.likes&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>
<br>

<h4>
<a href="#Passing-a-Boolean" class="headerlink" title="Passing a Boolean" data-scroll="">Passing a Boolean</a>
</h4>

<pre><code class="language-html  line-numbers">&#x3C;!-- Including the prop with no value will imply &#x60;true&#x60;. --&#x3E;
&#x3C;blog-post is-published&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Even though &#x60;false&#x60; is static, we need v-bind to tell Vue that --&#x3E;
&#x3C;!-- this is a JavaScript expression rather than a string.          --&#x3E;
&#x3C;blog-post v-bind:is-published=&#x22;false&#x22;&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Dynamically assign to the value of a variable. --&#x3E;
&#x3C;blog-post v-bind:is-published=&#x22;post.isPublished&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>
<br>


<h4>
<a href="#Passing-an-Array" class="headerlink" title="Passing an Array" data-scroll="">Passing an Array</a>
</h4>

<pre><code class="language-html  line-numbers">&#x3C;!-- Even though the array is static, we need v-bind to tell Vue that --&#x3E;
&#x3C;!-- this is a JavaScript expression rather than a string.            --&#x3E;
&#x3C;blog-post v-bind:comment-ids=&#x22;[234, 266, 273]&#x22;&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Dynamically assign to the value of a variable. --&#x3E;
&#x3C;blog-post v-bind:comment-ids=&#x22;post.commentIds&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>
<br>



<h4>
<a href="#Passing-an-Object" class="headerlink" title="Passing an Object" data-scroll="">Passing an Object</a>
</h4>

<pre><code class="language-html  line-numbers">&#x3C;!-- Even though the object is static, we need v-bind to tell Vue that --&#x3E;
&#x3C;!-- this is a JavaScript expression rather than a string.             --&#x3E;
&#x3C;blog-post
  v-bind:author=&#x22;{
    name: &#x27;Veronica&#x27;,
    company: &#x27;Veridian Dynamics&#x27;
  }&#x22;
&#x3E;&#x3C;/blog-post&#x3E;

&#x3C;!-- Dynamically assign to the value of a variable. --&#x3E;
&#x3C;blog-post v-bind:author=&#x22;post.author&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>


<br>
<h4>
<a href="#Passing-the-Properties-of-an-Object" class="headerlink" title="Passing the Properties of an Object" data-scroll="">Passing the Properties of an Object</a>
</h4>
<p>
اگر می خواهید تمام خصوصیات یک شی را به prop منتقل کنید ، می توانید از v-bind بدون آرگومان استفاده کنید v-bind به جای  v-bind: prop-name . به عنوان مثال:
</p>

<pre><code class="language-javascript  line-numbers">post: {
  id: 1,
  title: 'My Journey with Vue'
}
</code></pre>

<p>الگوی زیر :</p>
<pre><code class="language-html  line-numbers">&#x3C;blog-post v-bind=&#x22;post&#x22;&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>
<p>معادل است با :</p>

<pre><code class="language-html  line-numbers">&#x3C;blog-post
  v-bind:id=&#x22;post.id&#x22;
  v-bind:title=&#x22;post.title&#x22;
&#x3E;&#x3C;/blog-post&#x3E;
</code></pre>

<br>

<h3>جریان داده یک طرفه (One-Way Data Flow)</h3>
<p>
همه prop  ها از یک اتصال یک طرفه بین ویژگی های فرزند و والد  شکل می گیرند: وقتی ویژگی والد به روز شود ، به سمت فرزند  حرکت می کند ، اما برعکس اینچنین نیست. این باعث می شود کامپوننت های  فرزند  به طور تصادفی وضعیت والدین را تغییر ندهند ، که باعث می شود جریان داده های برنامه شما دشوارتر باشد.
</p>

<p>
علاوه بر این ، هر بار که  کانپوننت  والد به روز شود ، تمام prop  ها در کامپوننت فرزند با آخرین مقدار تازه می شوند. این بدان معناست که شما نباید prop  یک کامپوننت  فرزند را تغییر دهید. اگر این کار را انجام دهید ، Vue در کنسول به شما هشدار می دهد.
</p>

<p>
معمولاً دو حالت وجود دارد که وسوسه انگیز است که یک prop را تغییر دهید: 
</p>

<p>
<ul>
<li>
<p>
از prop برای عبور مقدار اولیه استفاده شود. بعد از آن ، کامپوننت فرزند از آن به عنوان یک ویژگی داده محلی استفاده می کند. در این حالت ، بهتر است یک ویژگی داده محلی را تعریف کنید که از prop به عنوان مقدار اولیه خود استفاده کند:
</p>
<pre><code class="language-javascript  line-numbers">props: [&#x27;initialCounter&#x27;],
data: function () {
  return {
    counter: this.initialCounter
  }
}
</code></pre>

</li>

<li>
<p>
چنانچه بخواهیم prop به عنوان یک مقدار  raw  منتقل شود که  نیاز به تغییر دارد. در این حالت ، بهتر است یک ویژگی computed را با عنوان مقدار prop تعریف کنید:
</p>
<pre><code class="language-javascript  line-numbers">props: [&#x27;size&#x27;],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
</code></pre>

</li>

</ul>
</p>

<blockquote class="has-icon tip">
<div>
توجه داشته باشید که objects  و arrays در JavaScript با استفاده از مرجع منتقل می شوند ، بنابراین اگر prop یک آرایه یا شی باشد ، تغییر دادن شی یا آرایه درون  کامپوننت فرزند بر وضعیت والد تأثیر می گذارد.
</div>
</blockquote>

<br>


<h3>Prop Validation</h3>
<p>
کامپوننت ها می توانند الزامات مربوط به prop های خود را تعیین کنند ، مانند انواع قبلاً مشاهده شده. چنانچه شرطی برآورده نشود    Vue در کنسول جاوا اسکریپت مرورگر به شما هشدار می دهد. این امر به ویژه در هنگام توسعه کامپوننت های در حال توسعه بسیار مفید است.
</p>

<p>
برای تعیین اعتبار سنجی ، می توانید به جای آرایه ای از رشته ها ، می توانید یک object را به همراه الزامات اعتبار سنجی ارائه دهید. مثلا:
</p>

<pre><code class="language-javascript  line-numbers">Vue.component(&#x27;my-component&#x27;, {
  props: {
    // Basic type check (&#x60;null&#x60; and &#x60;undefined&#x60; values will pass any type validation)
    propA: Number,
    // Multiple possible types
    propB: [String, Number],
    // Required string
    propC: {
      type: String,
      required: true
    },
    // Number with a default value
    propD: {
      type: Number,
      default: 100
    },
    // Object with a default value
    propE: {
      type: Object,
      // Object or array defaults must be returned from
      // a factory function
      default: function () {
        return { message: &#x27;hello&#x27; }
      }
    },
    // Custom validator function
    propF: {
      validator: function (value) {
        // The value must match one of these strings
        return [&#x27;success&#x27;, &#x27;warning&#x27;, &#x27;danger&#x27;].indexOf(value) !== -1
      }
    }
  }
})
</code></pre>

<p>
هنگامی که اعتبار سنجی مورد تایید نبود ، Vue یک هشدار کنسول تولید می کند .
</p>

<blockquote class="has-icon tip">
<div>
توجه داشته باشید که prop  ها قبل از ایجاد نمونه کامپوننت تأیید می شوند ، بنابراین خصوصیات نمونه (به عنوان مثال data ، computed و غیره) در داخل توابع پیش فرض یا اعتبارسنج در دسترس نخواهند بود.
</div>
</blockquote>

<br>

<h3>Prop Validation</h3>
<p>
نوع داده می تواند یکی از سازندگان بومی زیر باشد:
</p>
<p>
<ul style="direction: ltr">
<li>String</li>
<li>Number</li>
<li>Boolean</li>
<li>String</li>
<li>Array</li>
<li>Object</li>
<li>Date</li>
<li>Function</li>
<li>Symbol</li>
</ul>

</p>
<p>
علاوه بر این ، type همچنین می تواند سازنده سفارشی تابع باشد و با یک instanceof   بررسی می شود. به عنوان مثال ، با توجه به عملکرد سازنده زیر:
</p>

<pre><code class="language-javascript  line-numbers">function Person (firstName, lastName) {
  this.firstName = firstName
  this.lastName = lastName
}
</code></pre>

<P>
می توانید اینطور استفاده کنید :
</P>

<pre><code class="language-javascript  line-numbers">Vue.component(&#x27;blog-post&#x27;, {
  props: {
    author: Person
  }
})
</code></pre>

<P>
جهت تأیید مقدار author prop  ایجاد شده با  new Person .
</P>

<br>

<h3>Non-Prop Attributes</h3>
<p>
 non-prop attribute  خاصیتی است که به یک کامپوننت منتقل می شود ، اما prop مربوطه تعریف نشده است.
</p>
<p>
در حالی که props  های صریحاً تعریف شده برای انتقال اطلاعات به یک کامپوننت فرزند  ترجیح داده می شوند ، نویسندگان کتابخانه های کامپوننت همیشه نمی توانند زمینه هایی را که ممکن است کامپوننت های شان در آنها استفاده شود پیش بینی کنند. به همین دلیل کامپوننت ها می توانند صفات دلخواه را که به عنصر کامپوننت root اضافه می شوند ، بپذیرند.
</p>

<p>
به عنوان مثال ، تصور کنید که ما از یک کامپوننت 3rd-party  به نام  bootstrap-date-input   به همراه پلاگین  Bootstrap  که نیاز به  ویژگی data-date-picker در input نیاز دارد استفاده می کنیم. ما می توانیم این ویژگی را به نمونه کامپوننت خود اضافه کنیم :
</p>

<pre><code class="language-html  line-numbers">&#x3C;bootstrap-date-input data-date-picker=&#x22;activated&#x22;&#x3E;&#x3C;/bootstrap-date-input&#x3E;
</code></pre>

<p>
و ویژگی  data-date-picker="activated"  بصورت اتوماتیک به المان روت bootstrap-date-input اضافه خواهد شد.
</p>

<br>

<h3>Replacing/Merging with Existing Attributes</h3>
<p>
 قالب زیر را برای bootstrap-date-input تصور کنید :
</p>

<pre><code class="language-html  line-numbers">&#x3C;input type=&#x22;date&#x22; class=&#x22;form-control&#x22;&#x3E;
</code></pre>
<p>
جهت تعیین یک قالب برای پلاگین date picker  ، ممکن است لازم باشد class  خاصی اضافه کنیم ، مانند این:
</p>

<pre><code class="language-html  line-numbers">&#x3C;bootstrap-date-input
  data-date-picker=&#x22;activated&#x22;
  class=&#x22;date-picker-theme-dark&#x22;
&#x3E;&#x3C;/bootstrap-date-input&#x3E;
</code></pre>

<p>
در این حالت ، دو مقدار متفاوت برای class  تعریف می شود:
</p>

<ul>
<li>
form-control که توسط کامپوننت در الگوی خود تنظیم شده است :
</li>
<li>
date-picker-theme-dark که توسط والد آن به کامپوننت منتقل می شوند :
</li>
</ul>

<p>
برای بیشتر ویژگی ها ، مقدار ارائه شده به کامپوننت جایگزین مقادیر تعیین شده توسط کامپوننت خواهد شد. بنابراین به عنوان مثال ،   type = "text" جایگزین type = "date"  می شود و احتمالاً آن را می شکند! خوشبختانه ، ویژگی های class  و style  کمی هوشمند تر هستند ، بنابراین هر دو مقدار با هم ادغام می شوند و مقدار نهایی را می سازند. form-control date-picker-theme-dark : 
</p>

<br>

<h3>Disabling Attribute Inheritance</h3>
<p>
اگر نمی خواهید عنصر ریشه یک کامپوننت ویژگی ها را به ارث برساند ، می توانید inheritAttrs: false را در کامپوننت تنظیم نمایید. برای مثال :
</p>

<pre><code class="language-javascript  line-numbers">Vue.component(&#x27;my-component&#x27;, {
  inheritAttrs: false,
  // ...
})
</code></pre>

<p>
این به ویژه می تواند در ترکیب با نمونه ویژگی $attrs  که شامل نام ویژگی ها و مقادیر منتقل شده به یک کامپوننت است مفید باشد ، مانند موارد زیر:
</p>

<pre><code class="language-javascript  line-numbers">{
  required: true,
  placeholder: &#x27;Enter your username&#x27;
}
</code></pre>

<p>
با  inheritAttrs: false و $attrs ، می توانید به صورت دستی تصمیم بگیرید که کدام ویژگی را می خواهید منتقل کنید ، که اغلب برای کامپوننت پایه مطلوب است:
</p>


<pre><code class="language-javascript  line-numbers">Vue.component(&#x27;base-input&#x27;, {
  inheritAttrs: false,
  props: [&#x27;label&#x27;, &#x27;value&#x27;],
  template: &#x60;
    &#x3C;label&#x3E;
      {{ label }}
      &#x3C;input
        v-bind=&#x22;$attrs&#x22;
        v-bind:value=&#x22;value&#x22;
        v-on:input=&#x22;$emit(&#x27;input&#x27;, $event.target.value)&#x22;
      &#x3E;
    &#x3C;/label&#x3E;
  &#x60;
})
</code></pre>

<blockquote class="has-icon tip">
<div>
توجه داشته باشید که گزینه inheritAttrs: false  بر روی style  و class  انقیاد شده (bindings) تاثیری نمی گذارد.
</div>
</blockquote>

<p>
این الگو به شما امکان می دهد از کامپوننت های پایه بیشتر شبیه عناصر raw HTML استفاده کنید ، بدون اینکه به این عنصر توجه کنید که ریشه اصلی آن چیست:
</p>


<pre><code class="language-javascript  line-numbers">&#x3C;base-input
  label=&#x22;Username:&#x22;
  v-model=&#x22;username&#x22;
  required
  placeholder=&#x22;Enter your username&#x22;
&#x3E;&#x3C;/base-input&#x3E;
</code></pre>