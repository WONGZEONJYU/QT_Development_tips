# QT开发一些小技巧函数

本笔记可能没有固定的顺序

>```c++
>#include <QMetaEnum>
>#include <QString>
>
>
>/*获取枚举类型名和枚举值的名
>例如: ProcessState::NotRunning
>ProcessState枚举类型
>NotRunning枚举值
>*/
>
>template<typename T>
>typename std::enable_if<QtPrivate::IsQEnumHelper<T>::Value, QString>::type
>getEnumTypeAndValueName(T enumValue)
>{
>    auto metaObj{ qt_getEnumMetaObject(enumValue) };
>    auto EnumTypename{ qt_getEnumName(enumValue) };
>
>    const auto enumIndex { metaObj->indexOfEnumerator(EnumTypename) };
>    auto metaEnum { metaObj->enumerator(enumIndex) };
>
>    auto enumValueName { metaEnum.valueToKey(enumValue) };
>
>    return QString("%1::%2").arg(EnumTypename).arg(enumValueName);
>}
>```

