# recoil

## Recoilについて

 - Reactの状態管理ライブラリのひとつ

## Reduxとの違い

 - 状態管理ライブラリのひとつであるReduxは、Stateを管理しているStoreがひとつ。そのため、ひとつ更新があるとその他のコンポーネントでも影響を受ける
 - 一方で、RecoilはReduxでいうStoreをAtomとして、そのAtomを複数持つことができる。したがって、Atomで更新をかけたときに、そのAtomを利用してるコンポーネントのみ影響を受ける

## useContextとの違い

 - Reactのhook useContextはComonentのrootにproviderを作る
 - 子のCompoonentで更新をかけた場合、そのrootのコンポーネントがレンダリングされる。
 - さらにその子とrootコンポーネントの間のコンポーネントもレンダリングされる。つまり、context配下の全てのコンポーネントがレンダリングされる

## 使い方

 - states/　で各Atomを作成
 - RecoilRoot でAtomを利用するComponentをwrap
 - componentに `useRecoilValue`、`useSetRecoilState`、 あるいはそれらを統合した `useRecoilState` を読み込む


### Atomの使い方

atomを作成

```
import { atom } from 'recoil'

export const InpiutTitleState = atom({
  key: 'InpiutTitleState',
  default: ''
})
```

componentで受け取る

```
import { useRecoilValue } from "recoil";

const inpiutTitle = useRecoilValue(InpiutTitleState)
```

atomを更新する

```
import { atom } from 'recoil'

export const InpiutTitleState = atom({
  key: 'InpiutTitleState',
  default: ''
})
```

componentで更新する

```
import { useSetRecoilState } from "recoil";

const setInputTitle = useSetRecoilState(inputTitleState);

const handleChange = (e) => {
  setInputTitle(e.target.value);
},

return (
  <input
    type="text"
    onChange={handleChange}
  />
);
```

 - useRecoilValueとuseSetRecoilStateを統合する書き方
 - useRecoilStateを使う

```
import { useRecoilState } from "recoil";

const [inputTitle, setInputTitle] = useRecoilState(inputTitleState)
```

atomに対して処理を加える場合、selectorを使う

```
import { atom, selector } from "recoil";

export const addTitleState = atom({
  key: "addTitleState",
  default: [],
});

export const addTitleStateLength = selector({
  key: "addTitleStateLength",
  get: ({ get }) => {
    const addTitleState = get(addTitleState); // 対象のatomを指定
    return addTitleState?.length || 0;
  },
});
```

## 参考サイト

 - [【Recoil入門】１からReactの状態管理ライブラリのRecoilを学んでみよう](https://www.youtube.com/watch?v=S93hsNFmIcM)
