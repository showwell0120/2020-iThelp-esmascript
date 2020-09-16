# [Day02] ECMAScript 與 Javascript

> 你說你學的是 Javascript ，我說我 follow ES 標準來開發。  
> 我們 到底是不是同路人?

## 認識 Ecma International

![ecma](https://ecma-international.org/images/logo_printerf.jpg)

Ecma International ，前名為 European Computer Manufacturers Association(歐洲電腦製造商協會)，是一個制定電腦硬體、通訊、程式語言標準的非營利組織。由於這幾十年來訂定的大量標準，多被採納為國際標準。為了因應國際化，才改為現名。

在程式語言的領域中，這個組織訂定很多有名而且廣為應用的規範，像是 C#、C++，以及本系列的主題 - ECMAScript、到近幾年逐漸備受注目的 Dart 等。

## ECMAScript 的誕生

YURI 現在可以靠 Javascript~~混口飯吃~~作為一技之長，最重要的人物就是 Netscape 的 前技術長 [Brendan Eich](https://zh.wikipedia.org/wiki/%E5%B8%83%E8%98%AD%E7%99%BB%C2%B7%E8%89%BE%E5%85%8B)。在他待在 Netscape 的這段期間，為了能優化瀏覽器的互動效果，開發出輕量、腳本式的語言，並且命名為 Mocha。

那後來又怎麼會叫做 Javascript 呢?

Netscape 內部因為考量這個語言有參考到 Java 的一些特性，所以後來就以 Javascript 的名稱公開發布。在這之後提交給 Ecma International 進行標準化，代號為 ECMA-262，並且定義這個標準的名稱為 ECMAScript。

## ECMAScript 的實現

有了 ECMAScript 的標準出現，加上開發需求的增加，各家公司便積極發展各自的語言，像是微軟的 JScript、VBScript，跟 Adobe 的 ActionScript 等。

近幾年發展下來，Javascript 比其他後進語言的實現度來的高，加上 Google 開發的 V8 引擎和 NodeJS 的大幅應用，讓 Javascript 成為 ECMAScript 最主要的實現。在 WEB 開發上，已經成為不可或缺的角色之一。

## ECMAScript 的進化

前端工程師近幾年最有感的，除了 UI 框架以外，應該就是幾乎每年一變的 ESXXXX。到底這些新語法都是誰來制定的呢？

### TC-39

![tc-39](https://avatars1.githubusercontent.com/u/1725583?s=200&v=4)

TC-39(Technical Committee No.39)是 Ecma International 底下負責制定 ECMAScript 標準的機構。

在初期的時候，因為工作流程傳統，而且當時有多方角力試圖影響，中間最長有 10 年的時間處於停滯的狀態。

後來一些重量級公司的人物的加入、以及現代化開發的需求遽增，他們精簡修訂的過程，並且使用[Github](https://github.com/tc39)促進開源社區的參與。讓 ECMAScript 的發展再度活躍起來。

目前從一個提案出來到納入下一版的標準，通常會依序進行以下階段 ─

#### Stage0 (Strawperson)

由 TC-39 的成員提出，或有其他人向機構提交且並還沒否決的討論或想法。

目前在官方 Github 的 [Stage 0 Proposals](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md)看到的有:

- [以`::`取代`function.bind(this)`](https://github.com/tc39/proposal-bind-operator)
- [巢狀 import 宣告](https://github.com/benjamn/reify/blob/master/PROPOSAL.md)

等至少 10 多項提案。

#### Stage1 (Proposal)

已正式成為提案，並持續觀察與其他提案的相互影響。提案本身要有主要的語法描述、使用範例等具體內容。

目前在官方 Github 的 [Stage 1 Proposals](https://github.com/tc39/proposals/blob/master/stage-1-proposals.md)看到的有:

- [Observable 實現觀察者模式](https://github.com/tc39/proposal-observable)
- [`Promise.try`優化錯誤處理](https://github.com/tc39/proposal-promise-try)

等至少 60 多個提案。

這個階段的部分提案會有提供 polyfill 或 library 的實現，有興趣的人也可以找來試玩看看。

#### Stage2 (Draft)

提案已有初步的文稿，並且可能會有 Javascript 引擎(like V8)或是編譯器(like Babel)提供實驗性的功能來實現。

例如 [`Intl.DurationFormat` 取得持續時間](https://github.com/tc39/proposal-intl-duration-format)

#### Stage3 (Candidate)

這個階段已經成為侯選提案，等待機構和相關貢獻者的簽呈。這時內容不會有太多改變，並且確定至少會有瀏覽器的原生支持、polyfill 或轉譯器可以支持。

例如 [`Intl.DisplayNames` 顯示語言、區域、貨幣等翻譯](https://github.com/tc39/proposal-intl-duration-format)

目前在官方 Github 的文件中，stage2 跟 stage3 列表的統整在[這裡](https://github.com/tc39/proposals/tree/master/ecma402)

#### Stage4 (Finished)

當規範至少通過兩個驗收測試，就會進到這個階段，並且等待下一版釋出時，成為修訂的內容之一。

像是預計 2021 年發布的 [`Promise.any`](https://github.com/tc39/proposal-promise-any)

目前在官方 Github 的 [Finished Proposals](https://github.com/tc39/proposals/blob/master/finished-proposals.md) 可以查看。

### 題外話 - Babel

如果你跟 YURI 一樣使用 babel 或 webpack+babel-loader 轉譯程式，而且想在專案中使用還在 stage 階段的語法特性的話，可以到[官方 Github](https://github.com/babel/babel/tree/master/packages)找`plugin-proposal-`開頭的目錄，然後安裝下來。

接著在設定檔裡的`plugin`加入就好囉

```javascript
options: {
    plugins: [
            '@babel/plugin-proposal-function-bind',
            '@babel/plugin-proposal-async-generator-functions',
        ],
}
```

## 目前版本總覽

| 版號  | 發布日期    | 描述                                                                                                  |
| ----- | ----------- | ----------------------------------------------------------------------------------------------------- |
| 1     | 1997.6      | 初版                                                                                                  |
| 2     | 1998.6      | 修正格式以符合國際標準                                                                                |
| **3** | **1999.12** | **重大版本，為大家熟悉的 ES3。主要新增功能完整的正規表達式、例外處理等**                              |
| 4     | -------     | 政治因素和分歧被停擺 10 年。其中部分內容成為下一版標準                                                |
| **5** | **2009.12** | **重大版本, 為大家熟悉的 ES5。主要新增嚴格模式(strict mode)**                                         |
| 5.1   | 2011.6      | 修正格式以符合國際標準                                                                                |
| **6** | **2015.6**  | **重大版本，因要求須每年做一次版本的釋出，所以往後的正式名稱成為 ES 加上西元年份。正式名稱為 ES2015** |
| 7     | 2016.6      | 正式名稱為 ES2016                                                                                     |
| 8     | 2017.6      | 正式名稱為 ES2017                                                                                     |
| 9     | 2018.6      | 正式名稱為 ES2018                                                                                     |
| 10    | 2019.6      | 正式名稱為 ES2019                                                                                     |
| 11    | 2020.6      | 正式名稱為 ES2020                                                                                     |
| Next  | -------     | 為下一版釋出前的通稱                                                                                  |

## 小結

經過今天的整理，希望大家都能對 ECMAScript 的發展以及與 Javascipt 的關係有更進一步的認識。明天開始會介紹從 ES2015 以來的主要語法，敬請期待囉!

## 參考資源

- [MDN - ECMA](https://developer.mozilla.org/zh-TW/docs/Glossary/ECMA)
- [Wiki - Ecma 國際](https://zh.wikipedia.org/wiki/Ecma%E5%9B%BD%E9%99%85)
- [Wiki - ECMAScript](https://zh.wikipedia.org/wiki/ECMAScript)
- [重新認識 JavaScript: Day 02 JavaScript 簡介](https://ithelp.ithome.com.tw/articles/10190685)
- [TC39，ECMAScript 和 JavaScript 的未来](https://medium.com/@justjavac/tc39-ecmascript-proposals-future-of-javascript-386b12149880) -[從 ES6 規範看 JavaScript 的現在和未來](https://www.ithome.com.tw/news/99160)
- [JavaScript —  到底什么是？ ES6, ES8, ES 2017, ECMAScript 又是什么 ?](https://www.zcfy.cc/article/javascript-wtf-is-es6-es8-es-2017-ecmascript)
- [JavaScript 引擎 V8 发布 8.1 版本](https://www.colabug.com/2020/0227/7049052/)
