# recoil

## Recoilについて

 - Reactの状態管理ライブラリのひとつ

## Reduxとの違い

 - 状態管理ライブラリのひとつで、ReduxはStateを管理しているStoreがひとつ
 - 一方で、RecoilはReduxでいうStoreをAtomとして、そのAtomを複数持つことができる。したがってAtomが更新されると、そのAtomを利用してるコンポーネントのみrederingする

## useContextとの違い

 - Reactのhook useContextはComonentのrootにproviderを作る
 - 子のCompoonentが更新されると、そのrootのコンポーネントがレンダリングされる。
 - 複数useContextの値をお互いに持ち、更新することができない？Recoilでは `selector` を使って、複数のAtomの値で新しいdataを作ることができる
 
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
import { InpiutTitleState } from './state/input'

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
import { InpiutTitleState } from './state/input'

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
import { InpiutTitleState } from './state/input'

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
