# एयरबीएनबी CSS/Sass स्टाइलगाइड

_के लिए एक ज्यादातर उचित दृष्टिकोण CSS और Sass_

## विषयसूची

1. [Terminology](#terminology)
   - [Rule Declaration](#rule-declaration)
   - [Selectors](#selectors)
   - [Properties](#properties)
1. [CSS](#css)
   - [Formatting](#formatting)
   - [Comments](#comments)
   - [OOCSS and BEM](#oocss-and-bem)
   - [ID Selectors](#id-selectors)
   - [JavaScript hooks](#javascript-hooks)
   - [Border](#border)
1. [Sass](#sass)
   - [Syntax](#syntax)
   - [Ordering](#ordering-of-property-declarations)
   - [Variables](#variables)
   - [Mixins](#mixins)
   - [Extend directive](#extend-directive)
   - [Nested selectors](#nested-selectors)
1. [Translation](#translation)
1. [License](#license)

## शब्दावली

### नियम घोषणा

एक "नियम घोषणा" एक चयनकर्ता (या चयनकर्ताओं के समूह) को गुणों के साथ समूह के साथ दिया गया नाम है। यहाँ एक उदाहरण है:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selectors

एक नियम घोषणा में, "selectors" बिट्स हैं जो निर्धारित करते हैं कि DOM ट्री में कौन से तत्व परिभाषित गुणों द्वारा स्टाइल किए जाएंगे। चयनकर्ता HTML तत्वों के साथ-साथ तत्व के वर्ग, आईडी या इसके किसी भी गुण से मेल खा सकते हैं। यहाँ चयनकर्ताओं के कुछ उदाहरण दिए गए हैं:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

अंत में, गुण वे हैं जो नियम के चयनित तत्वों को उनकी शैली घोषित करते हैं। गुण कुंजी-मूल्य जोड़े हैं, और एक नियम घोषणा में एक या अधिक संपत्ति घोषणाएं हो सकती हैं। संपत्ति घोषणाएं इस तरह दिखती हैं:

```css
/* some selector */
 {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ back to top](#table-of-contents)**

## CSS

### Formatting

- इंडेंटेशन के लिए सॉफ्ट टैब्स (2 स्पेस) का इस्तेमाल करें।
- कक्षा के नामों में कैमलकेसिंग की तुलना में डैश को प्राथमिकता दें।
  - यदि आप बीईएम का उपयोग कर रहे हैं तो अंडरस्कोर और पास्कलकेसिंग ठीक है (देखें [OOCSS and BEM](#oocss-and-bem) नीचे)।
- आईडी चयनकर्ताओं का प्रयोग न करें।
- नियम घोषणा में एकाधिक चयनकर्ताओं का उपयोग करते समय, प्रत्येक चयनकर्ता को अपनी पंक्ति दें।
- नियम घोषणाओं में ओपनिंग ब्रेस `{` से पहले एक स्पेस रखें।
- गुणों में, `:` वर्ण के बाद, लेकिन पहले नहीं, एक स्थान रखें।
- नई लाइन पर नियम घोषणाओं के क्लोजिंग ब्रेसेस `}` लगाएं।
- नियम घोषणाओं के बीच खाली पंक्तियां डालें।

**Bad**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}
.no,
.nope,
.not_good {
  // ...
}
#lol-no {
  // ...
}
```

**Good**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Comments

- टिप्पणियों को ब्लॉक करने के लिए लाइन टिप्पणियों (सास-भूमि में `//`) को प्राथमिकता दें।
- उनकी अपनी लाइन पर टिप्पणियों को प्राथमिकता दें। अंत की पंक्ति टिप्पणियों से बचें।
- कोड के लिए विस्तृत टिप्पणियाँ लिखें जो स्व-दस्तावेजीकरण नहीं है:
  - जेड-इंडेक्स का उपयोग
  - संगतता या ब्राउज़र-विशिष्ट हैक

### OOCSS and BEM

हम इन कारणों से OOCSS और BEM के कुछ संयोजन को प्रोत्साहित करते हैं:

- यह CSS और HTML के बीच स्पष्ट, सख्त संबंध बनाने में मदद करता है
- यह पुन: प्रयोज्य, संयोजन योग्य घटक बनाने में हमारी सहायता करता है
- यह कम नेस्टिंग और कम विशिष्टता की अनुमति देता है
- यह स्केलेबल स्टाइलशीट बनाने में मदद करता है

**OOCSS**, या "ऑब्जेक्ट ओरिएंटेड CSS", CSS लिखने का एक तरीका है जो आपको अपनी स्टाइलशीट को "ऑब्जेक्ट्स" के संग्रह के रूप में सोचने के लिए प्रोत्साहित करता है: पुन: प्रयोज्य, दोहराए जाने योग्य स्निपेट जो पूरी वेबसाइट में स्वतंत्र रूप से उपयोग किए जा सकते हैं।

- Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
- Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, या "ब्लॉक-एलिमेंट-मॉडिफ़ायर", HTML और CSS में कक्षाओं के लिए एक _नामकरण परंपरा_ है। यह मूल रूप से यैंडेक्स द्वारा बड़े कोडबेस और स्केलेबिलिटी को ध्यान में रखते हुए विकसित किया गया था, और OOCSS को लागू करने के लिए दिशानिर्देशों के एक ठोस सेट के रूप में काम कर सकता है।

- CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
- Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

हम PascalCaseed "ब्लॉक" के साथ BEM के एक संस्करण की अनुशंसा करते हैं, जो विशेष रूप से घटकों (जैसे रिएक्ट) के साथ संयुक्त होने पर अच्छी तरह से काम करता है। संशोधक और बच्चों के लिए अभी भी अंडरस्कोर और डैश का उपयोग किया जाता है।

**उदाहरण**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">
      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>
    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard {
}
.ListingCard--featured {
}
.ListingCard__title {
}
.ListingCard__content {
}
```

- `.ListingCard` "ब्लॉक" है और उच्च-स्तरीय घटक का प्रतिनिधित्व करता है
- `.ListingCard__title` एक "तत्व" है और `.ListingCard` के वंश का प्रतिनिधित्व करता है जो ब्लॉक को समग्र रूप से बनाने में मदद करता है।
- `.ListingCard--featured` एक "संशोधक" है और `.ListingCard` ब्लॉक पर एक अलग स्थिति या भिन्नता का प्रतिनिधित्व करता है।

### ID selectors

जबकि सीएसएस में आईडी द्वारा तत्वों का चयन करना संभव है, इसे आम तौर पर एक विरोधी पैटर्न माना जाना चाहिए। आईडी चयनकर्ता अनावश्यक रूप से उच्च स्तर का परिचय देते हैं [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)आपके नियम घोषणाओं के लिए, और वे पुन: प्रयोज्य नहीं हैं।

इस विषय पर अधिक जानकारी के लिए पढ़ें [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) विशिष्टता से निपटने पर।

### JavaScript hooks

अपने सीएसएस और जावास्क्रिप्ट दोनों में एक ही कक्षा के लिए बाध्य होने से बचें। दोनों को परस्पर मिलाने से, कम से कम, रिफैक्टरिंग के दौरान समय बर्बाद होता है, जब एक डेवलपर को प्रत्येक वर्ग को क्रॉस-रेफरेंस देना चाहिए जो वे बदल रहे हैं, और सबसे खराब, डेवलपर्स को कार्यक्षमता टूटने के डर से बदलाव करने से डर लगता है।

हम बाइंड करने के लिए जावास्क्रिप्ट-विशिष्ट क्लास बनाने की सलाह देते हैं, जिसके साथ प्रीफ़िक्स्ड है`.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

यह निर्दिष्ट करने के लिए कि शैली की कोई सीमा नहीं है, `none` के बजाय `0` का उपयोग करें।

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```

**[⬆ back to top](#table-of-contents)**

## Sass

### Syntax

- `.scss` सिंटैक्स का उपयोग करें, कभी भी मूल `.sass` सिंटैक्स का उपयोग न करें
- अपने नियमित सीएसएस और `@include` घोषणाओं को तार्किक रूप से ऑर्डर करें (नीचे देखें)

### Ordering of property declarations

1. संपत्ति की घोषणा

   सभी मानक संपत्ति घोषणाओं को सूचीबद्ध करें, कुछ भी जो `@include` या नेस्टेड चयनकर्ता नहीं है।

   ```scss
   .btn-green {
     background: green;
     font-weight: bold;
     // ...
   }
   ```

2. `@include` घोषणाएं

   ग्रुपिंग `@include` अंत में पूरे चयनकर्ता को पढ़ना आसान बनाता है।

   ```scss
   .btn-green {
     background: green;
     font-weight: bold;
     @include transition(background 0.5s ease);
     // ...
   }
   ```

3. नेस्टेड चयनकर्ता

   नेस्टेड चयनकर्ता, _यदि आवश्यक हो_, अंत में जाएं, और उनके बाद कुछ भी नहीं जाता है। अपने नियम घोषणाओं और नेस्टेड चयनकर्ताओं के साथ-साथ आसन्न नेस्टेड चयनकर्ताओं के बीच व्हाइटस्पेस जोड़ें। अपने नेस्टेड चयनकर्ताओं पर ऊपर दिए गए समान दिशानिर्देश लागू करें।

   ```scss
   .btn {
     background: green;
     font-weight: bold;
     @include transition(background 0.5s ease);

     .icon {
       margin-right: 10px;
     }
   }
   ```

### Variables

कैमलकेस्ड या स्नेक_केस्ड वेरिएबल नामों पर डैश-केस्ड वेरिएबल नामों (जैसे `$my-variable`) को प्राथमिकता दें। वेरिएबल नामों को प्रीफ़िक्स करना स्वीकार्य है, जिनका उपयोग केवल उसी फ़ाइल में अंडरस्कोर के साथ किया जाना है (उदाहरण के लिए `$_my-variable`)।

### Mixins

मिक्सिन्स का उपयोग आपके कोड को सुखाने के लिए किया जाना चाहिए, स्पष्टता, या अमूर्त जटिलता को जोड़ने के लिए - उसी तरह से नामित कार्यों के समान। मिक्सिन जो कोई तर्क स्वीकार नहीं करते हैं, इसके लिए उपयोगी हो सकते हैं, लेकिन ध्यान दें कि यदि आप अपने पेलोड (जैसे gzip) को कंप्रेस नहीं कर रहे हैं, तो यह परिणामी शैलियों में अनावश्यक कोड दोहराव में योगदान दे सकता है।

### Extend directive

`@extend` से बचना चाहिए क्योंकि इसमें अनपेक्षित और संभावित रूप से खतरनाक व्यवहार है, खासकर जब नेस्टेड चयनकर्ताओं के साथ प्रयोग किया जाता है। यदि चयनकर्ताओं का क्रम बाद में बदल जाता है (उदाहरण के लिए यदि वे अन्य फ़ाइलों में हैं और फ़ाइलों को लोड किए जाने के क्रम में शिफ्ट किया जाता है) तो शीर्ष-स्तरीय प्लेसहोल्डर चयनकर्ताओं का विस्तार करने में भी समस्याएँ हो सकती हैं। गज़िपिंग को `@extend` का उपयोग करके आपके द्वारा प्राप्त की जाने वाली अधिकांश बचत को संभालना चाहिए, और आप अपनी स्टाइलशीट को मिश्रण के साथ अच्छी तरह से सुखा सकते हैं।

### Nested selectors

**चयनकर्ताओं को तीन स्तरों से अधिक गहरा न करें!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

जब चयनकर्ता इतने लंबे हो जाते हैं, तो संभावना है कि आप CSS लिख रहे हैं:

- HTML (नाज़ुक) से मज़बूती से जुड़ा हुआ _—या—_
- अत्यधिक विशिष्ट (शक्तिशाली) _—या—_
- पुन: प्रयोज्य नहीं

दोबारा: **नेवर नेस्ट आईडी सिलेक्टर्स!**

यदि आपको पहली बार एक आईडी चयनकर्ता का उपयोग करना चाहिए (और आपको वास्तव में ऐसा नहीं करना चाहिए), तो उन्हें कभी भी नेस्टेड नहीं होना चाहिए। यदि आप खुद को ऐसा करते हुए पाते हैं, तो आपको अपने मार्कअप पर दोबारा गौर करने की जरूरत है, या यह पता लगाने की जरूरत है कि इतनी मजबूत विशिष्टता की आवश्यकता क्यों है। यदि आप अच्छी तरह से निर्मित HTML और CSS लिख रहे हैं, तो आपको ऐसा करने की **कभी** आवश्यकता नहीं है।

**[⬆ back to top](#table-of-contents)**

## Translation

यह स्टाइल गाइड अन्य भाषाओं में भी उपलब्ध है:

- ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
- ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
- ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
- ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
- ![ka](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Georgia.png) **Georgian**: [DavidKadaria/css-style-guide](https://github.com/davidkadaria/css-style-guide)
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
- ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
- ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
- ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
- ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [rtplv/airbnb-css-ru](https://github.com/rtplv/airbnb-css-ru)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
- ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
- ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)
- ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [tderflinger/css-styleguide](https://github.com/tderflinger/css-styleguide)
- ![in](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/India.png) **हिंदी**: [sauravmeghwal/css-hindi](https://github.com/sauravmeghwal/css-hindi)

**[⬆ back to top](#table-of-contents)**

## License

(The MIT License)

Copyright (c) 2015 Airbnb

किसी भी व्यक्ति को इस सॉफ़्टवेयर और संबंधित दस्तावेज़ फ़ाइलों ('सॉफ़्टवेयर') की एक प्रति प्राप्त करने वाले किसी भी व्यक्ति को बिना किसी प्रतिबंध के सॉफ़्टवेयर में डील करने की अनुमति दी जाती है, जिसमें बिना किसी सीमा के उपयोग करने, कॉपी करने, संशोधित करने, मर्ज करने के अधिकार शामिल हैं। , सॉफ़्टवेयर की प्रतियां प्रकाशित, वितरित, सबलाइसेंस, और/या बेचना, और उन व्यक्तियों को अनुमति देना जिन्हें सॉफ़्टवेयर ऐसा करने के लिए प्रस्तुत किया गया है, निम्नलिखित शर्तों के अधीन:

उपरोक्त कॉपीराइट नोटिस और यह अनुमति नोटिस सॉफ्टवेयर की सभी प्रतियों या पर्याप्त भागों में शामिल किया जाएगा।

सॉफ़्टवेयर किसी भी प्रकार की वारंटी के बिना 'जैसा है' प्रदान किया जाता है, व्यक्त या निहित, जिसमें व्यापारिकता, किसी विशेष उद्देश्य के लिए उपयुक्तता और गैर-उल्लंघन की वारंटी शामिल है, लेकिन इन्हीं तक सीमित नहीं है। किसी भी घटना में लेखक या कॉपीराइट धारक किसी भी दावे, नुकसान या अन्य देयता के लिए उत्तरदायी नहीं होंगे, चाहे अनुबंध की कार्रवाई में, टोर्ट या अन्यथा, सॉफ़्टवेयर या उपयोग या अन्य व्यवहार के संबंध में या उससे उत्पन्न हो सॉफ़्टवेयर।

**[⬆ back to top](#table-of-contents)**
