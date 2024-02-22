# react-native

ReactNative 테스트

`study.git/프론트/ReactNative/환경구축.md` 내용 참고!

## React Native IOS 실행

`애플 M2 탑재된 맥OS의 경우에는 npm run ios 명령을 실행하기 전에 다음 작업을 수행`해야 합니다.

VSCode 에서 ios/Podfile 열고,

```
# Note that if you have use_frameworks! enabled, Flipper will not work and
# you should disable the next line.
```

위 주석을 찾아 다음 라인의 코드를 주석처리 합니다. (Flipper)

다음으로 터미널에서 프로젝트 내부의 ios 디렉토리로 이동한 뒤, ios 에서 사용하는 라이브러리를 설치

```bash
$ cd ios
$ pod install
$ cd ../
$ npm run ios
```

또는

```bash
$ cd ios
$ rm -rf Pods
$ rm -rf Podfile.lock
$ pod install
```

1. Xcode를 프로젝트명.xcworkspace 로 열어줍니다. (예: react-native.git/app/ios/app.xcworkspace)
2. Product > Clean Build Folder 를 실행합니다.
3. ▶︎ 를 눌러 실행합니다.

또는

homebrew 등으로 관련 도구(Node.js 또는 NVM 등)을 설치하면서,
ios 폴더 내부 NVM 버전세팅이 돌아가는 코드의 문제가 있을 수 있음.
이 경우, 'npx react-native init app' CLI 명령으로 프로젝트 다시 생성

https://reactnative.dev/docs/environment-setup?platform=ios&package-manager=yarn#optional-using-a-specific-version-or-template

또는

공식페이지 가이드에 따라 진행  
iOS에 문제가 있는 경우 다음을 실행하여 종속성을 다시 설치해 보세요.

https://reactnative.dev/docs/environment-setup?platform=ios&package-manager=yarn#creating-a-new-application

- 'cd ios' 폴더로 이동합니다.
- 'bundle install' 번들러를 설치
- 'bundle exec pod install' CocoaPods 에서 관리하는 iOS 종속성을 설치

```
Run instructions for Android:
• Have an Android emulator running (quickest way to get started), or a device connected.
• cd "react-native.git/app" && npx react-native run-android

Run instructions for iOS:
• cd "react-native.git/app/ios"

    • Install Cocoapods
      • bundle install # you need to run this only once in your project.
      • bundle exec pod install
      • cd ..

    • npx react-native run-ios
    - or -
    • Open app/ios/app.xcodeproj in Xcode or run "xed -b ios"
    • Hit the Run button

Run instructions for macOS:
• See https://aka.ms/ReactNativeGuideMacOS for the latest up-to-date instructions.
```

# react-strict-dom

https://github.com/facebook/react-strict-dom

https://github.com/facebook/react-strict-dom/blob/main/packages/react-strict-dom/COMPATIBILITY.md

App.js

https://github.com/facebook/react-strict-dom/blob/main/apps/examples/src/App.js

```tsx
/**
 * Copyright (c) Meta Platforms, Inc. and affiliates.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 *
 * @flow strict-local
 */

import * as React from "react";
import { ScrollView } from "react-native";
import { css, html } from "react-strict-dom";
import { tokens } from "./tokens.stylex";

type ExampleBlockProps = $ReadOnly<{
  title: string;
  children: React.Node;
}>;

const egStyles = css.create({
  container: { borderTopWidth: 1 },
  h1: { padding: 10, backgroundColor: "#eee" },
  content: { padding: 10 },
  div: {
    paddingBottom: 50,
    paddingTop: 50,
    backgroundColor: "white",
  },
});

function ExampleBlock(props: ExampleBlockProps) {
  const { title, children } = props;
  return (
    <html.div style={egStyles.container}>
      <html.h1 style={egStyles.h1}>{title}</html.h1>
      <html.div style={egStyles.content}>{children}</html.div>
    </html.div>
  );
}

const BGCOLOR_INACTIVE = "red";
const BGCOLOR_ACTIVE = "blue";

const TRANSLATE_NONE = "translateX(0px)";
const TRANSLATE_RIGHT = "translateX(150px)";

const SCALE_INACTIVE = "translateX(0px) scale(1)";
const SCALE_ACTIVE = "translateX(150px) scale(0.25)";

const ROTATE_INACTIVE = "rotate(0deg)";
const ROTATE_ACTIVE = "rotate(45deg)";

const SKEW_INACTIVE = "skewX(0deg)";
const SKEW_ACTIVE = "skewX(35deg)";

type ClickEventData = {
  altKey: boolean;
  button: ?number;
  ctrlKey: boolean;
  metaKey: boolean;
  pageX: ?number;
  pageY: ?number;
  shiftKey: boolean;
};

export default function App(): React.MixedElement {
  const [clickData, setClickData] = React.useState({ color: "red", text: "" });
  const [clickEventData, setClickEventData] = React.useState<ClickEventData>({
    altKey: false,
    ctrlKey: false,
    metaKey: false,
    shiftKey: false,
    button: null,
    pageX: null,
    pageY: null,
  });
  const [imageLoadText, setImageLoadText] = React.useState("");
  const [imageErrorText, setImageErrorText] = React.useState("");
  const [backgroundColor, setBackgroundColor] =
    React.useState(BGCOLOR_INACTIVE);
  const [opacity, setOpacity] = React.useState(1);
  const [transform, setTransform] = React.useState(TRANSLATE_NONE);
  const [scale, setScale] = React.useState(SCALE_INACTIVE);
  const [toggleTransform, setToggleTransform] = React.useState(false);
  const [rotate, setRotate] = React.useState(ROTATE_INACTIVE);
  const [skew, setSkew] = React.useState(SKEW_INACTIVE);
  const [fadeUpActive, setFadeUpActive] = React.useState(true);
  const [animate, setAnimate] = React.useState(false);

  return (
    <ScrollView>
      <html.div style={egStyles.div}>
        <ExampleBlock title="HTML elements">
          <html.div data-testid="testid">div</html.div>
          <html.span suppressHydrationWarning={true}>span</html.span>
          <html.p>paragraph</html.p>

          <html.div />

          <html.span>
            <html.a href="https://google.com">anchor</html.a>,
            <html.code>code</html.code>,<html.em>em</html.em>,
            <html.strong>strong</html.strong>,
            <html.span>
              H<html.sub>2</html.sub>0
            </html.span>
            ,<html.span>
              E=mc<html.sup>2</html.sup>
            </html.span>
          </html.span>

          <html.div />

          <html.pre>pre</html.pre>

          <html.div />

          <html.h1>h1</html.h1>
          <html.h2>h2</html.h2>
          <html.h3>h3</html.h3>
          <html.h4>h4</html.h4>
          <html.h5>h5</html.h5>
          <html.h6>h6</html.h6>

          <html.span>
            line <html.br /> break
          </html.span>
          <html.hr />

          {/* text inheritance and text children */}
          <html.div>Text inside div (kind of) works</html.div>
          <html.div style={styles.inheritedText}>
            <html.div>
              <html.span>Text style inheritance works</html.span>
            </html.div>
          </html.div>

          <html.img
            onLoad={(e) => {
              console.log(e.type, e);
            }}
            width={150}
            height={150}
            src="http://placehold.jp/150x150.png"
            style={styles.objContain}
          />

          <html.div />
          <html.label>label</html.label>
          <html.div />
          <html.button>button</html.button>
          <html.div />
          {/*<html.input placeholder="input type:date" type="date" />*/}
          <html.div />
          <html.input placeholder="input type:email" type="email" />
          <html.div />
          <html.input placeholder="input type:number" type="number" />
          <html.div />
          <html.input placeholder="input type:search" type="search" />
          <html.div />
          <html.input placeholder="input type:tel" type="tel" />
          <html.div />
          <html.input placeholder="input type:text" type="text" />
          <html.div />
          <html.input
            placeholder="input inputMode:numeric"
            inputMode="numeric"
          />
          <html.div />
          <html.input placeholder="input enterKeyHint:go" enterKeyHint="go" />
          <html.div />
          <html.select>
            <html.optgroup label="optgroup">
              <html.option label="option 1" />
              <html.option label="option 2" />
              <html.option label="option 3" />
            </html.optgroup>
          </html.select>
          <html.div />
          <html.textarea placeholder="textarea" />
        </ExampleBlock>

        {/* block layout emulation */}
        <ExampleBlock title="Variables & Theming">
          <html.p style={styles.inheritedText}>Global variables</html.p>
          <html.div style={styles.square} />

          <html.p style={[themedTokens, styles.inheritedText]}>
            Direct theming
          </html.p>
          <html.div style={[themedTokens, styles.square]} />

          <html.div style={themedTokens}>
            <html.p style={styles.inheritedText}>Inherit theming</html.p>
            <html.div style={styles.square} />
          </html.div>

          <html.div style={themedTokens}>
            <html.div style={themedTokensAlt}>
              <html.p style={styles.inheritedText}>Nested theming</html.p>
              <html.div style={styles.square} />
            </html.div>
          </html.div>
        </ExampleBlock>

        {/* block layout emulation */}
        <ExampleBlock title="Layout">
          <html.p>display:block emulation</html.p>
          <html.div>
            <html.div style={styles.square} />
            <html.div style={[styles.square, { backgroundColor: "blue" }]} />
          </html.div>

          {/* flex row undoes block layout emulation and correct flex child layout */}
          <html.p>display:flex defaults and children</html.p>
          <html.div style={styles.row}>
            <html.div style={[styles.square, styles.w1000]} />
            <html.div style={[styles.square, styles.blueSquare]}>
              <html.div style={styles.whiteBox}>
                <html.p>Back to block</html.p>
                <html.div style={styles.square} />
                <html.div style={[styles.square, styles.bgGreen]} />
              </html.div>
            </html.div>
          </html.div>

          <html.p>display:block resets flex properties</html.p>
          {/* display block undoes row layout and emulates block again */}
          <html.div style={[styles.row, styles.blockW300]}>
            <html.div style={styles.square} />
            <html.div style={[styles.square, styles.bgBlue]} />
          </html.div>

          {/* block and inline layout emulation */}
          <html.p>
            display:inline within display:block is{" "}
            <html.strong>not</html.strong> emulated
          </html.p>
          <html.div>
            <html.div style={styles.redBox}>
              <html.div style={styles.greenBox} />
              <html.span style={styles.bgYellow}>one</html.span>
              <html.span style={styles.bgYellow}>two</html.span>
            </html.div>
            <html.span style={styles.bgYellow}>one</html.span>
            <html.span style={styles.bgYellow}>two</html.span>
            <html.div style={styles.redBox} />
          </html.div>
        </ExampleBlock>

        {/* positioning (static by default) */}
        <ExampleBlock title="Position">
          <html.div style={[styles.p50, styles.relative]}>
            <html.div style={styles.p50}>
              <html.div style={[styles.square, styles.absTopLeft]} />
            </html.div>
            <html.div style={[styles.relative, styles.p50]}>
              <html.div style={[styles.square, styles.absTopLeft]} />
            </html.div>
          </html.div>
        </ExampleBlock>

        {/* event emulation */}
        <ExampleBlock title="Events">
          <html.input
            onChange={(e) => {
              console.log(e.type, e.target.value);
            }}
            onKeyDown={(e) => {
              console.log(e.type, e.key);
            }}
            onInput={(e) => {
              console.log(e.type, e.target.value);
            }}
          />
          <html.textarea
            onChange={(e) => {
              console.log(e.type, e.target.value);
            }}
            onKeyDown={(e) => {
              console.log(e.type, e.key);
            }}
            onInput={(e) => {
              console.log(e.type, e.target.value);
            }}
          />
          <html.div
            onClick={(e) => {
              setClickData((data) => ({
                color: data.color === "red" ? "blue" : "red",
                text: "click",
              }));
              setClickEventData({
                altKey: e.altKey,
                button: e.button,
                ctrlKey: e.ctrlKey,
                metaKey: e.metaKey,
                pageX: e.pageX,
                pageY: e.pageY,
                shiftKey: e.shiftKey,
              });
            }}
            style={[styles.h100, styles.dynamicBg(clickData.color)]}
          >
            <html.span style={styles.bgWhite}>{clickData.text}</html.span>
            <html.div style={styles.flex}>
              <html.div style={styles.flexGrow}>
                <html.div>
                  <html.span>
                    {clickEventData.altKey ? "✅" : "🚫"} altKey
                  </html.span>
                </html.div>
                <html.div>
                  <html.span>
                    {clickEventData.ctrlKey ? "✅" : "🚫"} ctrlKey
                  </html.span>
                </html.div>
                <html.div>
                  <html.span>
                    {clickEventData.metaKey ? "✅" : "🚫"} metaKey
                  </html.span>
                </html.div>
                <html.div>
                  <html.span>
                    {clickEventData.shiftKey ? "✅" : "🚫"} shiftKey
                  </html.span>
                </html.div>
              </html.div>
              <html.div style={styles.flexGrow}>
                <html.div>
                  <html.span>button: {clickEventData.button}</html.span>
                </html.div>
                <html.div>
                  <html.span>pageX: {clickEventData.pageX}</html.span>
                </html.div>
                <html.div>
                  <html.span>pageY: {clickEventData.pageY}</html.span>
                </html.div>
              </html.div>
            </html.div>
          </html.div>

          <html.img
            onLoad={(e) => {
              setImageLoadText(`${e.type}: loaded`);
            }}
            width={150}
            height={150}
            src="http://placehold.jp/150x150.png"
            style={styles.objContain}
          />
          <html.span>{imageLoadText}</html.span>
          <html.img
            onError={(e) => {
              setImageErrorText(`${e.type}: errored`);
            }}
            width={150}
            height={150}
            src="http://error"
            style={styles.objContain}
          />
          <html.span>{imageErrorText}</html.span>
        </ExampleBlock>

        {/* CSS Transitions Shim */}
        <ExampleBlock title="CSS Transitions">
          <html.p>Color</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionBackgroundColor,
              styles.dynamicBg(backgroundColor),
            ]}
          />
          <html.button
            onClick={() =>
              setBackgroundColor(
                backgroundColor === BGCOLOR_INACTIVE
                  ? BGCOLOR_ACTIVE
                  : BGCOLOR_INACTIVE
              )
            }
          >
            Toggle
          </html.button>

          <html.p>Opacity</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionOpacity,
              styles.dynamicOpacity(opacity),
            ]}
          />
          <html.button onClick={() => setOpacity(opacity === 0 ? 1 : 0)}>
            Toggle
          </html.button>

          <html.p>Translate</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionTransform,
              styles.dynamicTransform(transform),
            ]}
          />
          <html.button
            onClick={() =>
              setTransform(
                transform === TRANSLATE_NONE ? TRANSLATE_RIGHT : TRANSLATE_NONE
              )
            }
          >
            Toggle
          </html.button>

          <html.p>Translate and Scale</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionTransform,
              styles.dynamicTransform(scale),
            ]}
          />
          <html.button
            onClick={() =>
              setScale(scale === SCALE_INACTIVE ? SCALE_ACTIVE : SCALE_INACTIVE)
            }
          >
            Toggle
          </html.button>

          <html.p>Rotate</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionTransform,
              styles.dynamicTransform(rotate),
            ]}
          />
          <html.button
            onClick={() =>
              setRotate(
                rotate === ROTATE_INACTIVE ? ROTATE_ACTIVE : ROTATE_INACTIVE
              )
            }
          >
            Toggle
          </html.button>

          <html.p>Skew</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionTransform,
              styles.dynamicTransform(skew),
            ]}
          />
          <html.button
            onClick={() =>
              setSkew(skew === SKEW_INACTIVE ? SKEW_ACTIVE : SKEW_INACTIVE)
            }
          >
            Toggle
          </html.button>
          <html.p>Transform + Opacity</html.p>
          <html.div
            style={[
              styles.square,
              styles.transitionAll,
              styles.dynamicOpacity(fadeUpActive ? 1 : 0),
              styles.dynamicTransform(
                fadeUpActive ? "translateY(0)" : "translateY(100px)"
              ),
            ]}
          />
          <html.button onClick={() => setFadeUpActive(!fadeUpActive)}>
            Toggle
          </html.button>
        </ExampleBlock>
        <ExampleBlock title="Keyframe Animations">
          <html.div
            style={[
              styles.square,
              styles.bgRed,
              animate && styles.keyframeAnimation,
            ]}
          />
          <html.button onClick={() => setAnimate(!animate)}>
            {animate ? "Reset" : "Start"}
          </html.button>
        </ExampleBlock>
        <ExampleBlock title="Hover">
          <html.div style={styles.squareHover} />
        </ExampleBlock>
      </html.div>
    </ScrollView>
  );
}

const animateSequence = css.keyframes({
  "0%": {
    transform: "translateX(0px) rotate(0deg)",
  },
  "50%": {
    transform: "translateX(150px) rotate(0deg)",
  },
  "100%": {
    transform: "translateX(150px) rotate(180deg)",
  },
});

const themedTokens = css.createTheme(tokens, {
  squareColor: "purple",
  textColor: "purple",
});

const themedTokensAlt = css.createTheme(tokens, {
  squareColor: "orange",
  textColor: "darkorange",
});

const styles = css.create({
  keyframeAnimation: {
    animationDuration: "1s",
    animationIterationCount: 1,
    animationName: animateSequence,
    animationTimingFunction: "ease",
    transform: "translateX(150px)",
  },
  row: {
    display: "flex",
    borderColor: "black",
    borderStyle: "solid",
    borderWidth: 1,
  },
  square: {
    height: 100,
    width: 100,
    backgroundColor: tokens.squareColor,
  },
  squareHover: {
    height: 100,
    width: 100,
    backgroundColor: {
      default: "red",
      ":hover": "blue",
    },
  },
  inheritedText: {
    fontSize: 18,
    fontWeight: "bold",
    color: tokens.textColor,
  },
  paragraph: {
    marginBlock: 24,
    fontSize: 24,
  },
  transitionAll: {
    backgroundColor: "red",
    pointerEvents: "none",
    transitionDuration: "500ms",
    transitionProperty: "all",
    transitionTimingFunction: "ease",
  },
  transitionBackgroundColor: {
    backgroundColor: "red",
    transitionDuration: "500ms",
    transitionProperty: "backgroundColor",
    transitionTimingFunction: "ease",
  },
  transitionOpacity: {
    backgroundColor: "red",
    transitionDuration: "0.5s",
    transitionProperty: "opacity",
    transitionTimingFunction: "ease",
  },
  transitionTransform: {
    backgroundColor: "red",
    transitionDuration: "500ms",
    transitionProperty: "transform",
    transitionTimingFunction: "ease",
  },
  objContain: {
    objectFit: "contain",
  },
  flex: {
    display: "flex",
  },
  flexGrow: {
    flexGrow: 1,
  },
  blockW300: { width: 300, display: "block" },
  w1000: { width: 1000 },
  blueSquare: {
    backgroundColor: "blue",
    boxSizing: "border-box",
    height: "auto",
    width: 1000,
  },
  whiteBox: {
    marginTop: 10,
    backgroundColor: "white",
  },
  bgWhite: {
    backgroundColor: "white",
  },
  bgRed: {
    backgroundColor: "red",
  },
  bgGreen: {
    backgroundColor: "green",
  },
  bgBlue: {
    backgroundColor: "blue",
  },
  bgYellow: {
    backgroundColor: "yellow",
  },
  redBox: {
    padding: 50,
    backgroundColor: "red",
  },
  greenBox: {
    padding: 20,
    marginRight: 100,
    backgroundColor: "green",
  },
  p50: {
    padding: 50,
  },
  absTopLeft: {
    position: "absolute",
    top: 0,
    left: 0,
  },
  relative: {
    position: "relative",
  },
  h100: {
    height: 100,
  },
  dynamicBg: (color: string) => ({
    backgroundColor: color,
  }),
  dynamicOpacity: (opacity: number) => ({
    opacity,
  }),
  dynamicTransform: (transform: string) => ({
    transform,
  }),
});
```
