# Stream이란

프로그램은 외부에서 데이터를 읽거나 외부로 데이터를 출력하는 작업이 빈번하게 일어난다. 이때 데이터는 어떠한 통로를 통해 데이터가 이동되는데 이러한 통로를 Stream이라고 한다.

자바에서는 이러한 기능을 수행하기 위해 `InputStream` , `OutputStream` 을 제공하며, 단일 방향으로 연속적으로 이동한다.

- InputStream: 외부에서 데이터를 읽어 올때 사용
- OutputStream: 외부에서 데이터를 출력할 때 사용

```java
public abstract int read() throws IOException;
```

```java
public void read() throws IOException {
    
        byte[] bytes = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
        InputStream is = new ByteArrayInputStream(bytes);
        int data;
        while ((data = is.read()) != -1) {
            System.out.print(data);
        }
        
    }
```

- 입력 스트림에서 데이터를 1씩 읽고 읽은 데이터를 반환한다.
- 데이터를 다 읽으면 -1을 반환한다.

```java
출력
------------
1234567891011
```

```java
 public int read(byte buffer[]) throws IOException {
        return read(buffer, off, buffer.length);
    }
```

- 입력 스트림에서 buffer[off] 부터 buffer.length개 만큼 buffer에 저장 하고 읽은 데이터의 개수를 반환하고 더 이상 읽을 데이터가 없다면 -1을 반환

```java
public long skip(long n) throws IOException
```

- 읽을 데이터 중 n 바이트를 스킵하고 실제로 스킵한 바이트 개수가 반환된다.

```java
int available() throws IOException
```

- 읽은 데이터(바이트)가 얼마나 남았는지 반환

```java
public synchronized void mark(int readlimit) {}
```

- 되돌아갈 특정 위치를 마킹하는 메서드이다.
- readlimit은 현재 위치를 마킹하고 최대 몇개의 바이트를 더 읽을 수 있는지를 의미한다.

```java
public synchronized void reset() throws IOException {
   throw new IOException("mark/reset not supported");
}
```

# **OutputStream**

바이트 기반 출력 스트림의 최상위 추상클래스

```java
 public abstract void write(int b) throws IOException;

 public void write(byte b[]) throws IOException {
   write(b, 0, b.length);
}

```

```java
    public void write01() throws IOException {
        byte[] bytes = {9, 8, 7, 6, 5, 4, 3, 2, 1, 0};

        File file = new File("D://write_test.txt");
        OutputStream outputStream = new FileOutputStream(file);

        for (byte b : bytes) {
            outputStream.write(b);
        }

//바이트를 한번에 넣을 수 있다.//outputStream.write(bytes);

        outputStream.close();
    }
```

- 바이트 배열을 write_text.txt 파일에 write하는 예제.
- OutputStream을 상속받은 FileOutputStream을 생성하고, 한 바이트 씩 write하거나 여러 바이트씩 write 할 수 있다.

```java
public void write(byte b[], int off, int len) throws IOException
```

```java
    public void write() throws IOException {
        byte[] bytes = {9, 8, 7, 6, 5, 4, 3, 2, 1, 0, 7, 8, 7, 8, 5, 2, 4};
        int len = 3;
        int offset = 0;
        int total = bytes.length;

        File file = new File("D://write_test.txt");
        OutputStream outputStream = new FileOutputStream(file);

        while (total >= (offset + len)) {
            outputStream.write(bytes, offset, len);
            offset += len;
        }

        if (total - offset > 0) {
            outputStream.write(bytes, offset, total - offset);
        }

        outputStream.close();
    }
```

- byte 배열 b를 offset부터 len만큼 write한다.

```java
    public void read() throws IOException {

        File file = new File("D://write_test.txt");
        InputStream inputStream = new FileInputStream(file);
        int b;
        while ((b = inputStream.read()) != -1) {
            System.out.print(b);
        }

    }
```

- write_test.txt로 write한 데이터를 한 바이트씩 꺼내서 출력

---

```java
public void flush() throws IOException {}
```

- 버퍼를 지원하는 경우 버퍼에 존재하는 데이터를 목적지까지 보낸다.

---

```java
public void close() throws IOException {
}

```

- OutputStream을 종료

# IndexOf()

**indexOf()** 는 **특정 문자**나 **문자열**이 **앞에서부터 처음 발견되는 인덱스를 반환**하며

만약 **찾지 못했을 경우** **"-1"을 반환**합니다.

```java
 - indexOf(String str)

 - indexOf(int ch)

 - indexOf(int ch, int fromIndex)

 - indexOf(String str, int fromIndex)
```

# Substring()

문자열의 특정 부분을 잘라내는데 사용하는 메서드

```java
public String substring(int startIndex)
public String substring(int startIndex, int endIndex) // startIndex 부터 endIndex 전까지
```

# split()

split() 은 입력 받은 정규표현식 또는 특정 문자를 기준으로 문자열을 잘라 배열에 저장

```java
String str = "010-1234-5678";
String[] mobNum = str.split("-");
String ret1 = mobNum[0];
String ret2 = mobNum[1];
String ret3 = mobNum[2];

System.out.println("ret1 = "+ret1); // 010
System.out.println("ret2 = "+ret2); // 1234
System.out.println("ret3 = "+ret3); // 5678
```
