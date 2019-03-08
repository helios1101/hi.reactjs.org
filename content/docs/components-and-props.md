---
id: components-and-props
title: कौम्पोनॅन्ट तथा Props
permalink: docs/components-and-props.html
redirect_from:
  - "docs/reusable-components.html"
  - "docs/reusable-components-zh-CN.html"
  - "docs/transferring-props.html"
  - "docs/transferring-props-it-IT.html"
  - "docs/transferring-props-ja-JP.html"
  - "docs/transferring-props-ko-KR.html"
  - "docs/transferring-props-zh-CN.html"
  - "tips/props-in-getInitialState-as-anti-pattern.html"
  - "tips/communicate-between-components.html"
prev: rendering-elements.html
next: state-and-lifecycle.html
---

कौम्पोनॅन्टस हमें UI को स्वतंत्र, पुन: प्रयोज्य टुकड़ो में विभाजित करने में मदद करता है ,तथा
हर हिस्से को अलग मानता है. यह पन्ना कौम्पोनॅन्टस का परिचय देता है. आप खोज सकते है [ विस्तृत कौम्पोनॅन्ट API reference यहाँ पर](/docs/react-component.html).

सैद्धांतिक रूप से, कौम्पोनॅन्टस जावास्क्रिप्ट फंक्शन्स जैसा है. 
वे अर्बिट्ररी इनपुट्स स्वीकार करते है (जिससे "props" बुलाया जाता है ) और वापस आती है React एलिमेंट्स जो वर्णन करती है की स्क्रीन पर क्या आना चाहिए.

## फंक्शन्स तथा कौम्पोनॅन्टस {#function-and-class-components}

सबसे सरल तरीका एक कौम्पोनॅन्ट को परिभाषित करने की यह है की एक  जावास्क्रिप्ट फंक्शन्स लिखी जाए:

```js
function Welcome(props) {
  return <h1>नमस्ते, {props.name}</h1>;
}
```

यह फंक्शन्स एक वैध React कौम्पोनॅन्ट है क्योकि यह स्वीकार करता है एक अकेला "props" (which stands for properties) object argument with data और वापस आती है React एलिमेंट्स. हम उन कौम्पोनॅन्टस "फंक्शन्स कहते है  कौम्पोनॅन्टस "फंक्शन्स कौम्पोनॅन्टस" क्योकि वो वाकई में एक जावास्क्रिप्ट फंक्शन्स है.


आप भी उपयोग कर सकते हैं [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) का ताकि परिभाषित कर सके कौम्पोनॅन्ट को:

```js
class Welcome extends React.Component {
  render() {
    return <h1>नमस्ते, {this.props.name}</h1>;
  }
}
```

ऊपर के दोनों कौम्पोनॅन्टस बराबर है React's दृष्टिकोण से.

Classes की कुछ अतिरिक्त विशेषताएं भी हैं जिसकी हम चर्चा करेंगे [अगले खंड](/docs/state-and-lifecycle.html) में. तब तक, हम इस्तेमाल करेंगे फंक्शन्स कौम्पोनॅन्टस के संक्षिप्ति होने का.

## कौम्पोनॅन्ट रेंडरिंग {#rendering-a-component}

इससे पहले, हमने केवल वही React एलिमेंट्स का सामना किया जो DOM टैग्स का दर्शाता था:

```js
const element = <div />;
```

हालाँकि, एलिमेंट्स उपयोगकर्ता परिभाषित कौम्पोनॅन्टस को भी दर्शा सकते है:

```js
const element = <Welcome name="Sara" />;
```

जब कभी भी React देखता है एलिमेंट को यूजर-डिफाइंड  कौम्पोनॅन्ट का प्रतिनिधित्व करते हुए, यह JSX की विशेषताएँ पास करता है इस  कौम्पोनॅन्ट को एक object के रूप में. हम इस object को "props" कहते हैं .

उदाहरण के लिए, यह कोड पेज पर रेंडर करता है "नमस्ते, Sara" :

```js{1,5}
function Welcome(props) {
  return <h1>नमस्ते, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[](codepen://components-and-props/rendering-a-component)

चलो देकते है इस उदाहरण में क्या होता है:

1. हम बुलाते है `ReactDOM.render()` को `<Welcome name="Sara" />` एलिमेंट्स से.
2. React बुलाते है `Welcome` कौम्पोनॅन्ट को `name: 'Sara'}` के साथ props के रूप में.
3. यह `Welcome` रेंडरस और वापस आती है `<h1>नमस्ते, Sara</h1>` एलिमेंट परिणाम के तौर पर .
4. React DOM कुशलता पूर्वक DOM को अपडेट करता है `<h1>नमस्ते, Sara</h1>` से.

>**ध्यान दें:** हमेशा रेंडर की नाम की शुरुवात कैपिटल लेटर से होनी चाहिए.
>
>React उन कौम्पोनॅन्टस को जो लोअरकेस से स्टार्ट होते है उससे DOM टैग्स मानता है. उदाहरण के लिए, `<div />` HTML div टैग्स को दर्शाता है, पर `<Welcome />` दर्शाता है रेंडर को और ज़रुरत होती है `Welcome` को दायरे में होने की.
>
>इस सम्मेलन के पीछे तर्क के बारे में अधिक जानने के लिए, कृपया पढ़ें [JSX गहराई में](/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized).

## कौम्पोनॅन्टस लिखना {#composing-components}

कौम्पोनॅन्टस अन्य कौम्पोनॅन्टस का उल्लेख कर सकते हैं अपने आउटपुट में. इससे हम उसी रेंडरस का उपयोग कर सकते हैं, विस्तार के किसी भी स्तर के लिए. एक बटन, फॉर्म, डायलॉग, स्क्रीन: React अप्प्स में, वे सब को आमतौर पर कौम्पोनॅन्टस के रूप में व्यक्त किया जाता है.

उदाहरण के लिए, हम एक `App` बना सकते हैं जो रेंडरस करता है `Welcome` को कई बार:

```js{8-10}
function Welcome(props) {
  return <h1>नमस्ते, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

[](codepen://components-and-props/composing-components)

आम तौर पर, नया React अप्प्स के पास एक अकेला `App`  रेंडर होता है सबसे ऊपर में. हालाँकि, अगर आप एकीकृत करते हैं React को एक मौजूदा ऐप में, आप बेहद नीचे से छोटी चीज़ो के रेंडर्स से शुरुवात कर सकते हैं जैसे `Button` और धीरे-धीरे दृश्य पदानुक्रम के ऊपर तक जाते है.

## कौम्पोनॅन्टस निकालना {#extracting-components}

कौम्पोनॅन्टस को छोटे छोटे कौम्पोनॅन्टस में विभाजित करने से डरना नहीं चाहिए.

उदाहरण के लिए, इस पर विचार करो की `Comment` रेंडरस:

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

[](codepen://components-and-props/extracting-components)

यह स्वीकार करता है `author` (एक ऑब्जेक्ट), `text` (एक string), और `date` (एक date) जैसे props, और सोशल मीडिया वेबसाइट पर एक टिप्पणी का वर्णन करता है.

यह रेंडरस को बदलने के लिए मुश्किल हो सकता है क्योंकि एक के अंदर दूसरी संरचना के वजह से,तथा इसकी अकेली पार्ट्स का पुन: उपयोग करना भी कठिन है. चलो कुछ कौम्पोनॅन्टस निकालते हैं.

सबसे पहले, हम निकालेंगे `Avatar`:

```js{3-6}
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```
 

यह `Avatar` को जानने की जरूरत नहीं है कि यह एक `Comment` के अंदर रेंडर किया जा रहा है. इसलिए हमने इसके prop को एक ज्यादा सामान्य नाम दिया है : `author` के बजाय `user`.

Props की नामकरण हम रेंडर की अनुसार करने की सलाह देते हैं  बजाय उस संदर्भ में किया जाए जिसमें इसका उपयोग किया जा रहा है.

हम अब `Comment` को थोड़ा सरल कर सकते हैं:

```js{5}
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

अगला, हम एक निकालेंगे `UserInfo` रेंडर जो रेंडर करता है `Avatar` को जोकि user's name के पास है:

```js{3-8}
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

यह हमे `Comment` को और भी ज्यादा आसान बना देता है:

```js{4}
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

[](codepen://components-and-props/extracting-components-continued)

कौम्पोनॅन्टस निकालना पहली बार में ग्रंट काम लग सकता है, लेकिन पुन: प्रयोज्य कौम्पोनॅन्टस के एक पैलेट होना बड़े ऐप्स में भुगतान करता है. यह एक अच्छा व्यवहार है की अगर आपका UI के पार्ट कई बार इस्तेमाल किये गए है (`Button`, `Panel`, `Avatar`), या अपने आप में काफी जटिल है (`App`, `FeedStory`, `Comment`), 
यह पुन: प्रयोज्य कौम्पोनॅन्ट होने के लिए एक अच्छा उम्मीदवार है.

## Props केवल-पढ़ने के लिए हैं {#props-are-read-only}

चाहे आप ए की घोषणा करें कौम्पोनॅन्ट की [फंक्शन्स या class के जैसे](#function-and-class-components), 
इसे कभी भी संशोधित नहीं करना चाहिए खुदके props का. इस `sum` फंक्शन्स पर विचार करो:

```js
function sum(a, b) {
  return a + b;
}
```

यह फंक्शन्स को हम कहते है ["pure"](https://en.wikipedia.org/wiki/Pure_function) क्योंकि वे अपने इनपुट को बदलने का प्रयास नहीं करते हैं, और हमेशा समान इनपुट के लिए समान परिणाम लौटाते हैं. 

इसके विपरीत, यह फंक्शन्स impure है क्योंकि यह अपना इनपुट खुद बदलता है:

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

React बहुत लचीला है, लेकिन इसमें एक सख्त नियम है:

**सारे React कौम्पोनॅन्टस को pure फंक्शन्स की तरह कार्य करना चाहिए अपने props के अनुसार.**


बेशक, अनुप्रयोग UI गतिशील हैं और समय के साथ बदलते हैं. अब [अगले सेक्शन](/docs/state-and-lifecycle.html) 
में, हम एक नई अवधारणा पेश करेंगे "state". State React कौम्पोनॅन्टस को उपयोगकर्ता क्रियाओं के जवाब में समय के साथ अपने उत्पादन को बदलने के लिए अनुमति देता है, नेटवर्क प्रतिक्रियाएँ, और कुछ भी, इस नियम का उल्लंघन किए बिना.
