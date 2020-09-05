# Serializable

序列化就是把实体对象状态按照一定的格式写入到有序字节流。

反序列化就是从有序字节流重建对象，恢复对象状态。

## 1 序列化

对象序列化的主要作用是在传递和保存对象时保证对象的完整性和可传递性。

序列化是把对象转换成有序字节流，以便在网络上传输或者保存在本地文件中。

序列化后的字节流保存了Java对象的状态以及相关的描述信息。

序列化机制的核心作用就是对象状态的保存与重建。

```Java
		A a1 = new A(123, "abc");
		String objectFile = "assets/io/Serializable/a1";

		// 对象序列化存为文件
		FileOutputStream fos = new FileOutputStream(objectFile);
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(a1);
		oos.close();
```

## 2 反序列化

客户端从文件中或网络上获得序列化后的对象字节流后，根据字节流中所保存的对象状态及描述信息，通过反序列化重建对象。

```java
		String objectFile = "assets/io/Serializable/a1";
		// 文件反序列化为对象
		FileInputStream fis = new FileInputStream(objectFile);
		ObjectInputStream ois = new ObjectInputStream(fis);
		A a2 = (A) ois.readObject();
		ois.close();
		System.out.println(a2);//x = 123  y = abc
```

## 3 应用场景

当两个进程进行远程通信时，可以相互发送各种类型的数据，包括文本、图片、音频、视频等，这些数据都会以二进制序列的形式在网络上传送。

当两个Java进程进行通信时，就需要Java序列化与反序列化。

发送方把Java对象转换为字节序列，然后在网络上传送；接收方从字节序列中恢复出Java对象。

### 3.1序列化的优点

1. 永久性保存对象，保存对象的字节序列到本地文件或者数据库中；
2. 通过序列化以字节流的形式使对象在网络中进行传递和接收；
3. 通过序列化在进程间传递对象；

## 4 实现可序列化对象

实现序列化需实现Serializable或Externalizable接口，否则会抛出异常。

transient 关键字可以使一些属性不会被序列化。

```java
public class SerializableTest {

	private static class A implements Serializable {

		private int x;
		private String y;

		A(int x, String y) {
			this.x = x;
			this.y = y;
		}

		@Override
		public String toString() {
			return "x = " + x + "  " + "y = " + y;
		}
	}
}

```

