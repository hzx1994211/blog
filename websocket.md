
```websocket
// 重连定时器
let wsCreateHandler = null
const socket = {
  websocket: null,
  connectURL: process.env.SOCKET_URL,
  connectParam:'',//url参数
  // 开启标识
  socket_open: false,
  // 心跳timer
  hearbeat_timer: null,
  // 心跳发送频率
  hearbeat_interval: 10000,
  // 是否自动重连
  is_reonnect: true,
  // 重连次数
  reconnect_count: 5,
  // 已发起重连次数
  reconnect_current: 1,
  // 网络错误提示此时
  ronnect_number: 0,
  // 重连timer
  reconnect_timer: null,
  // 重连频率
  reconnect_interval: 5000,
  // 事件回调
  receiveMessage:null,
  init: () => {
    if (!('WebSocket' in window)) {
      // Toast.fail('浏览器不支持WebSocket');
      return null;
    }
    // 已经创建过连接不再重复创建
    // if (socket.websocket) {
    //   return socket.websocket
    // }
 
    socket.websocket = new WebSocket(`${socket.connectURL}${socket.connectParam}`);
    console.log(socket.websocket);
    socket.websocket.onmessage = (e) => {
      if (socket.receiveMessage) {
        socket.receiveMessage(e);
      }
    };

    socket.websocket.onclose = (e) => {
      clearInterval(socket.hearbeat_interval);
      socket.socket_open = false;
      // 需要重新连接
      if (socket.is_reonnect) {
        socket.reconnect_timer = setTimeout(() => {
          // 超过重连次数
          if (socket.reconnect_current > socket.reconnect_count) {
            clearTimeout(socket.reconnect_timer);
            socket.is_reonnect = false;
            return;
          }

          // 记录重连次数
          socket.reconnect_current++;
          socket.reconnect();
        }, socket.reconnect_interval);
      }
    };

    // 连接成功
    socket.websocket.onopen = function () {
      socket.socket_open = true;
      socket.is_reonnect = true;
      console.log('----链接成功');
      // 开启心跳
      socket.heartbeat();
    };

    // 连接发生错误
    socket.websocket.onerror = function (err) {
      console.log('----连接失败',`${socket.connectURL}${socket.connectParam}`,err);
    };
  },

  send: (data, callback = null) => {
    // 开启状态直接发送
    if (socket.websocket.readyState === socket.websocket.OPEN) {
       socket.websocket.send(data == 'PING' ? data : JSON.stringify(data));
      if (callback) {
        callback();
      }

      // 正在开启状态，则等待1s后重新调用
    } else {
      clearInterval(socket.hearbeat_timer);
      if (socket.ronnect_number < 1) {
        // Toast.fail('关闭demo');
      }
      socket.ronnect_number++;
    }
  },

  receive: (message) => {
    // let params = Base64.decode(JSON.parse(message.data).data); //解密
    const params = JSON.parse(message.data).date;
    return params;
  },

  heartbeat: () => {
    if (socket.hearbeat_timer) {
      clearInterval(socket.hearbeat_timer);
    }

    socket.hearbeat_timer = setInterval(() => {

      console.log('----心跳');
      socket.send('PING');
    }, socket.hearbeat_interval);
  },

  close: () => {
    clearInterval(socket.hearbeat_interval);
    clearInterval(socket.hearbeat_timer); //关闭心跳
    socket.is_reonnect = false;
    socket.websocket?.close();
    console.log('---关闭');
  },

  /**
   * 重新连接
   */
  reconnect: () => {
    if (socket.websocket && !socket.is_reonnect) {
      socket.close();
    }
    // 没连接上会一直重连，设置延迟避免请求过多
    wsCreateHandler && clearTimeout(wsCreateHandler)
    wsCreateHandler = setTimeout(() => {
      socket.init();
    }, 3000)
  },
};

export default socket;

# 引用 
websocket.connectParam = `jsonParam=${Base64.encode(JSON.stringify(publicParams))}&sign=${sign}` //参数
websocket.receiveMessage = this.receiveMessage
websocket.init()

methods ：{
	//消息接受
  async receiveMessage(response) { }
}

```

