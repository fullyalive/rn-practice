# **REACT NATIVE**

### Command

```
npx expo start : 서버 실행
```

### KeyboardAvoidingView
- 키보드 호출시 하단 키보드 높이를 기준으로 높이, 위치 또는 핟ㄴ 패딩을 자동으로 조정하는 View
- [docu](https://reactnative.dev/docs/keyboardavoidingview)
```
import React from 'react';
import {
  View,
  KeyboardAvoidingView,
  TextInput,
  StyleSheet,
  Text,
  Platform,
  TouchableWithoutFeedback,
  Button,
  Keyboard,
} from 'react-native';

const KeyboardAvoidingComponent = () => {
  return (
    <KeyboardAvoidingView
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
      style={styles.container}>
      <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
        <View style={styles.inner}>
          <Text style={styles.header}>Header</Text>
          <TextInput placeholder="Username" style={styles.textInput} />
          <View style={styles.btnContainer}>
            <Button title="Submit" onPress={() => null} />
          </View>
        </View>
      </TouchableWithoutFeedback>
    </KeyboardAvoidingView>
  );
};
```

### SafeAreaView

- 앱 헤더와 푸터만큼의 공간을 두고 시작하는 영역
- [React Navigation](https://velog.io/@byron1st/2%ED%8E%B8.-React-Navigation-%EC%84%A4%EC%B9%98)과 의존관계
- [docu](https://github.com/th3rdwave/react-native-safe-area-context)

```
import { SafeAreaProvider, SafeAreaView } from 'react-native-safe-area-context';

<SafeAreaProvider>
    <SafeAreaView
        style={styles.container}
        edges={['top', 'right', 'bottom', 'left']} // 예외없이 모두 안전영역 적용
    >
        <FlatList
          data={isOpened ? friendProfiles : []}
          contentContainerStyle={{ paddingHorizontal: 15 }}
          keyExtractor={(_, index) => index}
          stickyHeaderIndices={[0]}
          ItemSeparatorComponent={ItemSeparatorComponent}
          renderItem={renderItem}
          ListHeaderComponent={ListHeaderComponent}
          ListFooterComponent={ListFooterComponent}
          showsVerticalScrollIndicator={false}
        />
        <TabBar selectedTabIdx={selectedTabIdx} setSelectedTabIdx={setSelectedTabIdx} />
    </SafeAreaView>
</SafeAreaProvider>

import {Text, SafeAreaView} from 'react-native';

<SafeAreaView style={styles.container}>
    <Text style={styles.text}>Page content</Text>
</SafeAreaView>
```

### FlatList
- 많은 양의 스크롤이 필요한 리스트 아이템을 보여줄 때 사용 [ref](https://velog.io/@djaxornwkd12/React-Native-FlatList%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
- 화면 내에 보이는 영역에서만 데이터를 렌더링
- [docu](https://reactnative.dev/docs/flatlist)

```
import React, {useState} from 'react';
import {
  FlatList,
  SafeAreaView,
  StatusBar,
  StyleSheet,
  Text,
  TouchableOpacity,
} from 'react-native';

const DATA = [
  {
    id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
    title: 'First Item',
  },
  {
    id: '3ac68afc-c605-48d3-a4f8-fbd91aa97f63',
    title: 'Second Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Third Item',
  },
];

const Item = ({item, onPress, backgroundColor, textColor}) => (
  <TouchableOpacity onPress={onPress} style={[styles.item, {backgroundColor}]}>
    <Text style={[styles.title, {color: textColor}]}>{item.title}</Text>
  </TouchableOpacity>
);

const App = () => {
  const [selectedId, setSelectedId] = useState();

  const renderItem = ({item}) => {
    const backgroundColor = item.id === selectedId ? '#6e3b6e' : '#f9c2ff';
    const color = item.id === selectedId ? 'white' : 'black';

    return (
      <Item
        item={item}
        onPress={() => setSelectedId(item.id)}
        backgroundColor={backgroundColor}
        textColor={color}
      />
    );
  };

return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={item => item.id}
        extraData={selectedId}
      />
    </SafeAreaView>
);
```

### Icon

엑스포 제공 아이콘 [list](https://icons.expo.fyi/)

```
import { Ionicons } from '@expo/vector-icons';

<IconButton name="search-outline" />
<IconButton name="person-add-outline" />
<IconButton name="md-musical-notes-outline" />
<IconButton name="ios-settings-outline" />
```
