---
title: unity实战总结
date: 2017-01-15 20:23:39
tags: unity
---
主要是我在unity中遇到得一些问题总结。
<!--more-->
1.unity中的碰撞检测

*示例代码*
```c
using UnityEngine;
using System.Collections;

public class 碰撞 : MonoBehaviour {
       private Color colors;
       // Use this for initialization
       void Start () {b
       }

       // Update is called once per frame
       void Update () {

       }
       //满足刚体 和trriger
       void OnTriggerEnter(){
              float r = Random.Range(0f, 1f);
              float g = Random.Range(0f, 1f);
              float b = Random.Range(0f, 1f);
              colors = new Color(r,g,b);
              gameObject.GetComponent<Renderer>().material.color =colors;//改变颜色
       }

}

```
作为碰撞的物体必须有刚体（rigidbody）
作为碰撞检测的的物体必须有（collider）并且Is trigger属性为true

2.unity中的射线

```c
public LayerMask mask;
//射线检测碰到的层
public GameObject qiu;
//点击生成的物体

       void Update ()
          {
        RaycastHit hit1;
          //RaycastHit 光线投射碰撞
          //RaycastHit相关的变量    http://www.ceeger.com/Script/RaycastHit/RaycastHit.html
        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
          //ray 射线 .direction方向 origin射线原点
        if (Physics.Raycast(ray,out hit1,500f,mask) && Input.GetMouseButtonDown(0) )
        //Physics.Raycast 射线投射  起始点 射线方向  射线长度 射线投射的层 && 判断鼠标左键按下
         //从屏幕点的开开始射出一条加hit1的射线长度为500f，和mask层进行交互
        {
            Instantiate(qiu, hit1.point, Quaternion.identity);
            // raycastHit .point 返回射线与层碰到的世界坐标
        }
       }

```

3.获取游戏组件内的属性
```c
obj.GetComponent<Renderer> ().material.color = Color.red;
```

4.摄像机激活、关闭
```c
       cams [a].active = false;
```

5.复制游戏中物体
```c
utusing UnityEngine;
using System.Collections;

public class ss : MonoBehaviour {
       public GameObject man;
       private Vector3 p;
       // Use this for initialization
       void Start () {
              for(int i=0;i<9;i++){
                     for(int j=0;j<9;j++){
                           p = new Vector3 (i,0,j);
                           Instantiate (man,p,Quaternion.identity);//复制一个物体 物体，坐标，方向
                                  //Quaternion 四元数
                              //

                     }

              }

       }

       // Update is called once per frame
       void Update () {

       }
}
```
```Quaternion.identity```该四元数，相当于“无旋转”：这个物体完全对齐于世界或父轴。

6.控制游戏内的物体显示、隐藏
```c
object.gameObject.SetActive(true);
```

7.使用TextField
```c
//必须引入
using UnityEngine.UI;
//才可以定义
public InputField apassword;
string passwordd = apassword.text;
//里边的文本内容
```

8.在console里打印辅助信息
```c
print("hello world!");
```

9.设置定时器

让tip(text)显示一秒隐藏

```c
else {
                     tip.gameObject.SetActive (true);
                     StartCoroutine (DisapperMessage ());
     //开始协调程序
     //一个协同程序在执行过程中,可以在任意位置使用yield语句。yield的返回值控制何时恢复协同程序向下执行。
     //协同程序在对象自有帧执行过程中堪称优秀。协同程序在性能上没有更多的开销。
     //StartCoroutine函数是立刻返回的,但是yield可以延迟结果。直到协同程序执行完毕。
              }
       }

              IEnumerator DisapperMessage()
              {
     //中断指令
                     yield return new WaitForSeconds(1);
                     tip.gameObject.SetActive(false);
              }

```

10.unity添加mov格式的视频

前置条件：需要安装quicktime支持，把脚本挂在一个需要显示的平面上
```c
public MovieTexture movTexture;

void Update () {
              GetComponent<Renderer>().material.mainTexture = movTexture;
     //定义视频贴图
              movTexture.Play ();
     //播放视频
       }

```

11.unity场景跳转
```c
using UnityEngine.SceneManagement;

SceneManager.LoadScene(SceneName);
```

12.法线贴图

使用软件Crazybump进行制作
下图是使用方法
![](http://oi7f2yeu5.bkt.clouddn.com/fa1.png)
![](http://oi7f2yeu5.bkt.clouddn.com/fa2.png)

13.绕点旋转
```c
using UnityEngine;
using System.Collections;

public class rotate : MonoBehaviour {
    private Vector3 center = new Vector3(-48.6f,-70.0f,-89.3f);
       // Use this for initialization
       void Start () {

       }

       // Update is called once per frame
       void Update () {
        transform.RotateAround(center, Vector3.up, 20 * Time.deltaTime);
    }
}
```
围绕世界坐标的point点的axis旋转该变换angle度。
这个修改变换的位置和旋转角度。

14.简单位移
```c
  if (Vector3.Distance(target.transform.position, transform.position) > 0.1f)
  {
  Vector3 v = (target.transform.position - transform.position).normalized;
  Quaternion rot = Quaternion.LookRotation(v);
     //插值
  transform.rotation = Quaternion.Slerp(transform.rotation, rot, Time.deltaTime * speed);
  transform.position += transform.forward * Time.deltaTime;
  }
```

15.unity中定时器使用
```c
       void Update () {
        timer(time[1]);
       }
  

void timer(int data)
    {
            timer1 += Time.deltaTime;
            if (timer1 >= 1)
            {
                time[1]--;
                labelChangeInt(time[1], "time");
                timer1 = 0;
                print(data);
            }
//每一秒钟，执行一次代码
    }
```

16.C# 非void 带返回值的使用方法
```c
  Vector3 randomPos()
    {
        float x = Random.Range(0, planeWidth);
        float z = Random.Range(0, planeHeight);
        Vector3 random = new Vector3(x, 0, z);
        return random;
    }
```

17.切换天空盒
```c
public Material sky01;
RenderSettings.skybox=sky01;
```

18.通过间隔符，提取字符串
```c
   string test2 = "100-200-300";
        char[] separator = { '-' };
        string[] tests = test2.Split(separator);
     //Split里必须是char类型
        print(tests[1]);
```

20.提取字符串中的第i个字符开始的长度为j的字符串
```c
     string test1 = "100200300";
        print(test1.Substring(3,3));

//or
     string str = "GTAZB_JiangjBen_123";
     int start=3,length=8;
     print(str.Substring(start-1, length));
```
<a href="http://blog.csdn.net/fengqingtao2008/article/details/45082775">更多操作数据知识</a>

21.模型动画切换
```c
public bool run = false;
    public Animation thisA;
       // Use this for initialization
       void Start () {
        thisA = gameObject.GetComponent<Animation>();
     //获取animation组件
       }

       // Update is called once per frame
       void Update () {
        if (run == true)
        {
            print("切换动画");
            thisA.Play("run_");
        }
        else
        {
            thisA.Play("idle1_");
        }
       }
```

22.播放指定的声音片段

前置条件：添加Audio source组件并添加声音
```c
public AudioSource audio;
audio = gameObject.GetComponent<AudioSource>();
audio.PlayOneShot(audio.clip, 1.0f);
```

23.C#获取本机IP
```c
using System.Net.NetworkInformation;
using System.Net.Sockets;
//引入命名空间
 
        string userIp = "";
        NetworkInterface[] adapters = NetworkInterface.GetAllNetworkInterfaces(); ;
        foreach (NetworkInterface adapter in adapters)
        {
            if (adapter.Supports(NetworkInterfaceComponent.IPv4))
            {
                UnicastIPAddressInformationCollection uniCast = adapter.GetIPProperties().UnicastAddresses;
                if (uniCast.Count > 0)
                {
                    foreach (UnicastIPAddressInformation uni in uniCast)
                    {
                        //得到IPv4的地址。 AddressFamily.InterNetwork指的是IPv4
                        if (uni.Address.AddressFamily == AddressFamily.InterNetwork)
                        {
                            userIp = uni.Address.ToString();
                        }
                    }
                }
            }
        }

        print(userIp);
```


2017.1
未完待续......