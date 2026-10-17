
在本实验中，我们将测试 Shodan API。你需要一个 API key；由于我们没有使用任何过滤器，使用免费的 key 即可。在安装 CLI 后，我们将编写一个 Python 脚本来搜索横幅中包含“alarm”单词且位于美国的 MQTT 服务。该代码以及本章中的所有代码可以在书的下载网站和 GitHub 仓库上找到。

```python
% sudo apt install python3-venv
<truncated>
% python3 -m venv lab-19 && source ./lab-19/bin/activate
% pip install wheel
Collecting wheel
  Using cached wheel-0.36.2-py3-none-any.whl (35 KB)
  Installing collected packages: wheel
  Successfully installed wheel-0.36.2
% pip install shodan
Collecting shodan
  Downloading shodan-1.25.0.tar.gz (51 KB)
    51 KB 389 kB/s <truncated>
```

为了在不破坏系统 Python 库的情况下尝试新的 Python 库，安装 Python 3 虚拟环境（Virtual Environment）非常有帮助。

1. 安装一个新的虚拟环境并激活它。2. 为了减少在安装模块时关于未安装 wheel 的抱怨，我们安装了 wheel。

3. 此时，我们可以安装实验所需的任何模块，而不会污染我们的系统环境——例如 `shodan` 模块。4.

```python
% cat mqtt-search.py

def shodan_search():
    SHODAN_API_KEY = "YOUR API KEY"
    SEARCH = "mqtt alarm country:US"
    api = shodan.Shodan(SHODAN_API_KEY)

    try:
        results = api.search(SEARCH)
        with open("mqtt-results.txt", "w") as f:
            for result in results['matches']:
                searching = result['ip_str']
                f.write(searching + '\n')
    except shodan.APIError as e:
        pass

shodan_search()
```

接下来，我们运行 MQTT 搜索并观察结果：

```python
% python mqtt-search.py
% head -3 mqtt-results.txt
104.248.4.175
209.33.212.31
198.199.109.124
```

# 实验 19-3：玩转 MQTT

在上一个实验中，将字符串 `"mqtt alarm"` 提供给 Shodan，以识别运行 MQTT 带有警报监听的 IP 地址。在本实验中，我们将对结果中的一个 IP 进行扫描以获取额外信息。以下代码改编自 Victor Pasknel 的示例¹⁶。

```python
% pip install paho-mqtt
Collecting paho-mqtt
UsingUsing cached paho-mqtt-1.5.1.tar.gz (101 KB)
Building wheels for collected packages: paho-mqtt
Building wheel for paho-mqtt (setup.py) ... done
Created wheel for paho-mqtt: filename=paho-mqtt-1.5.1-py3-none-any.whl
size=61546 sha256-c11308bd024alb78dc47fba699d135d18544d2aba6283d9088ae4fe378667ff
Stored in directory: /home/kali/.cache/pip/wheels/22/b9/f0/9a1f646474f849b8a 
Successfully built paho-mqtt
Installing collected packages: paho-mqtt
Successfully installed paho-mqtt-1.5.1
% cat mqtt-scan.py
import paho.mqtt.client as mqtt
```

```python
def on_connect(client, userdata, flags, rc):
    print('[+] Connection successful')
    client.subscribe('#', qos = 1) # 订阅所有主题

def on_message(client, userdata, msg):
    print('[+] Topic: %s - Message: %s' % (msg.topic, msg.payload))

client = paho.mqtt.Client(client_id = "MqttClient")
client.on_connect = on_connect
client.on_message = on_message
client.connect('IP GOES HERE - MASKED', 1883, 30)
client.loop_forever()
```

这个 Python 程序非常简单：在加载 `mqtt.client` 库后，程序定义了初始连接的回调 1（打印连接消息并订阅服务器上的所有主题）以及接收到消息的回调 2（打印消息）。接下来，初始化客户端 3 并注册回调函数 4 5。最后，连接客户端 6（务必修改此行中的被遮蔽 IP）并进入循环 7。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_681_0.png)

注意：这里不涉及身份验证（遗憾的是），拍摄这部电影时没有小猫受到伤害！

接下来，我们运行 MQTT 扫描器：

```bash
root@kali:~# python mqtt-scan.py
[+] Connection successful
[+] Topic: /garage/door/ - Message: On

[+] Topic: owtracks/CHANGED/bartsimpson - Message:
  "type":"location","tid":"CHANGED","acc":5,"batt":"100","conn":"m","lat":-47.CHANGED00,"lon":-31.CHANGED00,"tst":"CHANGED","cp":true"
[+] Topic: home/alarm/select - Message: Disarm
[+] Topic: owtracks/CHANGED/bartsimpson - Message:
  "type":"location","tid":"CHANGED","acc":5,"batt":"100","conn":"m","lat":-47.CHANGED00,"lon":-31.CHANGED00,"tst":"CHANGED","cp":true"
```

## 无身份验证的含义

接下来，我们运行 MQTT 扫描器：

```python
import paho.mqtt.client as mqtt
```

# BullGuard 物联网扫描器

`iotscanner.bullguard.com/`

NIST 特别出版物 800-82，修订版2，“工业控制系统 (ICS) 安全指南”

`vlppubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-82r2.pdf`

“工业系统攻击面的量化评估与视觉化”

`www.cl.cam.ac.uk/~/fms27/papers/2011-Leverett-industrial.pdf`

### 参考文献

- 1. X. Xu，“服务创新中的物联网，”The Amfiteatu Economic Journal, 4(6, 2012年11月): 698–719.

- 2. M. Swan，“传感器狂热！物联网、可穿戴计算、客观指标与量化自我 2.0，”传感器与执行器网络杂志, 1(3, 2012年11月8日): 217–253.

- 3. Patrick Grossetete，“IoT 与网络：未来何何？,”Cisco, 2020年6月,https://blogs.cisco.com/networking/iot-and-the-network-what-is-the-future
