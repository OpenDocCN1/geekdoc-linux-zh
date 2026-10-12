
```
        "publisher": "O'Reilly Media, Inc.",

        "publishedDate": "2013-06-12",

        "description": "通过这本实战书籍获取对 Python 核心语言的全面深入介绍。",

        "imageLinks": {

          "SmallThumbnail": "http://books.google.com/books/content?id=4pgFXXckc&pcsrint=frontcover&img=1&zoom=5&edge=curl&source=gbs_api",

          "thumbnail": "http://books.google.com/books/content?id=4pgFXXckc&pcsrint=frontcover&img=1&zoom=1&edge="

        },

        "saleInfo": {

          "saleability": "FOR_SALE"

        }

      }

    }

  ]

}
```

## 构建 BookModel

让我们创建一个 `BookModel` 类来保存 API 电影列表数据集。`BookModel` 类将为 JSON 响应的每个属性拥有成员。

### `BookModel.fromJson(...)`

`BookModel.fromJson(Map<String, dynamic> json)` 接收一个 JSON 映射并将相应的值分配给 `BookModel` 对象的成员。这是调用解析从网络接收到的 JSON 响应的入口点。在这种情况下，JSON 响应属性是分层的。每一层将有它自己的模型。`BookModel` 类需要访问 `volumeInfo`、`accessInfo` 和 `saleInfo` 属性/成员。

### `BookModel` 类

`BookModel.fromJson()` 使用了工厂构造函数。当实现一个不总是创建类新实例的构造函数时，就会使用工厂构造函数。当从缓存获取对象而不是创建重复项时，它非常有用。

```dart
class BookModel {
  final VolumeInfo volumeInfo;
  final AccessInfo accessInfo;
  final SaleInfo saleInfo;
  BookModel({this.volumeInfo, this.accessInfo, this.saleInfo});
  factory BookModel.fromJson(Map<String, dynamic> json) {
    return BookModel(
      volumeInfo: VolumeInfo.fromJson(json['volumeInfo']),
      accessInfo: AccessInfo.fromJson(json['accessInfo']),
      saleInfo: SaleInfo.fromJson(json['saleInfo'])
    );
  }
}
```

## 数据建模

### `VolumeInfo` 类

`VolumeInfo` 类拥有 `title`、`authors` 作为其成员。它引用了 `ImageLinks` 类来获取 `thumbnail`。

```dart
class VolumeInfo {
  final String title;
  final String subtitle;
  final List<String> authors;
  final String publisher;
  final String publishedDate;
  final String description;
  VolumeInfo({this.title, this.subtitle, this.authors, this.publisher, this.publishedDate, this.description});
  factory VolumeInfo.fromJson(Map<String, dynamic> json) {
    return VolumeInfo(
      title: json['title'],
      subtitle: json['subtitle'],
      authors: json['authors'],
      publisher: json['publisher'],
      publishedDate: json['publishedDate'],
      description: json['description'],
    );
  }
}
```

```dart
class ImageLinks {
  final String smallThumbnail;
  final String thumbnail;
  ImageLinks({this.smallThumbnail, this.thumbnail});
  factory ImageLinks.fromJson(Map<String, dynamic> json) {
    return ImageLinks(
      smallThumbnail: json['SmallThumbnail'],
      thumbnail: json['thumbnail'],
    );
  }
}
```

```dart
class AccessInfo {
  final String webReaderLink;
  AccessInfo({this.webReaderLink});
  factory AccessInfo.fromJson(Map<String, dynamic> json) {
    return AccessInfo(
      webReaderLink: json['webReaderLink'],
    );
  }
}
```

```dart
class SaleInfo {
  final String saleability;
  final String buyLink;
  SaleInfo({this.saleability, this.buyLink});
  factory SaleInfo.fromJson(Map<String, dynamic> json) {
    return SaleInfo(
      saleability: json['saleability'],
      buyLink: json['buyLink'],
    );
  }
}
```

## 数据建模

### `AccessInfo` 类

`AccessInfo` 类提供了 `webReaderLink`，链接到：`http://play.google.com/books/reader?id=4pgFXXck&hl=en&print=frontcover&source=gbs_api`

```dart
class AccessInfo {
  final String webReaderLink;
  AccessInfo({this.webReaderLink});
  factory AccessInfo.fromJson(Map<String, dynamic> json) {
    return AccessInfo(
      webReaderLink: json['webReaderLink'],
    );
  }
}
```

### `SaleInfo` 类

`SaleInfo` 类提供了链接到：`https://play.google.com/store/books/detail`

```dart
class SaleInfo {
  final String saleability;
  final String buyLink;
  SaleInfo({this.saleability, this.buyLink});
  factory SaleInfo.fromJson(Map<String, dynamic> json) {
    return SaleInfo(
      saleability: json['saleability'],
      buyLink: json['buyLink'],
    );
  }
}
```

### `VolumeInfo` 类

`VolumeInfo` 类拥有 `title`、`authors` 作为其成员。它引用了 `ImageLinks` 类来获取 `thumbnail` 信息。

```dart
class VolumeInfo {
  final String title;
  final String subtitle;
  final List<String> authors;
```
