---
title: WebIM ����ָ��
sidebar: webimsidebar
secondnavwebim: true
---

# ��������  

## ��ʼ��

### ��������{#conn_new}
<pre class="hll"><code class="language-javascript">
var conn = new Easemob.im.Connection();
</code></pre>

### ��ʼ������{#conn_init}
<pre class="hll"><code class="language-javascript">
conn.init({
    https : true,//�Ǳ��urlֵδ����ʱ��Ч�����Ȳ���url���õĲ�����Ĭ�ϲ���http���ӣ���ַΪ��http://im-api.easemob.com/http-bind/��������httpsʱ���ݴ�ֵ����ַΪ����https://im-api.easemob.com/http-bind/��
    url �� 'http://im-api.easemob.com/http-bind/',//�Ǳ��Ĭ�������������ַ��
    domain : 'aa.com',//�Ǳ��Ĭ�ϣ���easemob.com��
    wait �� '60',//�Ǳ�����ӳ�ʱ��Ĭ�ϣ�60����λseconds
    onOpened : function() {
        curUserId = conn.context.userId;
        //��ѯ�����б�
        conn.getRoster(....);
    },
    onClosed : function() {
        //����ǳ��¼�
    },
    onTextMessage : function(message) {
        /**�����ı���Ϣ����Ϣ��ʽΪ��
            {	type :'chat',//Ⱥ��Ϊ��groupchat��
                from : from,
                to : too,
                data : { "type":"txt",
                    "msg":"hello from test2"
                }
            }
        */
        handleTextMessage(message);
    },
    onEmotionMessage : function(message) {
        /*���������Ϣ,��Ϣ��ʽΪ��
            {	type :'chat',//Ⱥ��Ϊ��groupchat��
                from : from,
                to : too,
                data : [{ "type":"txt",
                    "msg":"hello from test2"
                },
                { "type":"emotion",
                  "msg":"data:image/png;base64, ����"//ͼƬ��base64����
                }]
            }
        */
        handleEmotion(message);
    },
    onPictureMessage : function(message) {
        /**����ͼƬ��Ϣ����Ϣ��ʽΪ��
            {	type :'chat',//Ⱥ��Ϊ��groupchat��
                from : "test1",
                to : "test2",
                url : "http://s1.easemob.com/weiquan2/a2/chatfiles/0c0f5f3a-e66b-11e3-8863-f1c202c2b3ae",
                secret : "NSgGYPCxEeOou00jZasg9e-GqKUZGdph96EFxJ4WxW-qkxV4",
                filename : "logo.png",
                thumb : "http://s1.easemob.com/weiquan2/a2/chatfiles/0c0f5f3a-e66b-11e3-8863-f1c202c2b3ae",
                thumb_secret : "0595b06a-ed8b-11e3-9b85-93fade9c198c",
                file_length : 42394,
                width : 280,
                height : 160,
                filetype : "image/png",
                accessToken :"YWMtjPPoovCqEeOQs7myPqqaOwAAAUaqNH0a8rRj4PwJLQju6-S47ZO6wYs3Lwo"
            }
        */

        handlePictureMessage(message);
    },
    onAudioMessage : function(message) {
        /**������Ƶ��Ϣ����Ϣ��ʽΪ��
           {	type :'chat',//Ⱥ��Ϊ��groupchat��
                from : "test1",
                to : "test2",
                url : "http://s1.easemob.com/weiquan2/a2/chatfiles/0c0f5f3a-e66b-11e3-8863-f1c202c2b3ae",
                secret :"NSgGYPCxEeOou00jZasg9e-GqKUZGdph96EFxJ4WxW-qkxV4",
                filename : "��������.mp3",
                length :45223,
                file_length : 304,
                filetype : "mp3",
                accessToken :"YWMtjPPoovCqEeOQs7myPqqaOwAAAUaqNH0a8rRj4PwJLQju6-S47ZO6wYs3Lwo"
            }
        */
        handleAudioMessage(message);
    },
    //�յ���ϵ�˶�������Ļص�����
    onPresence : function (message){
        /**
            {
                from: "l2",
                fromJid: "easemob-demo#chatdemoui_l2@easemob.com",
                status: "����11:44:47",
                to: "test1",
                toJid: "easemob-demo#chatdemoui_test1@easemob.com/13856640471403797405809685",
                type: "subscribed"
            }
        */
        handlePresence(message);
    },
    //�յ���ϵ����Ϣ�Ļص�����
    onRoster : function (message){
        /**
            [{
                groups: [{0: "default",
                        length: 1}],
                jid: "easemob-demo#chatdemoui_l2@easemob.com",
                name: "l2",
                subscription: "to"
            }]
        */
        handleRoster(message);
    },
    onError : function(e) {
        //�쳣����
        alert(e.msg);
    }
});
</code></pre>

### ������{#conn_open}

֧��username/password��username/token��¼���ַ�ʽ��sdk�л���ݴ���Ĳ��������Զ�ѡ���Ƿ��¼usergrid����ȡ��¼�ɹ���token���ٽ��е�¼���죬���ʹ��token�Ĵ����ӽ�������¼usergird��ֱ�ӵ�¼IM��������

<pre class="hll"><code class="language-javascript">
//�û���
var user = $("#username").val();
//����
var pass = $("#password").val();
if (user == '' || pass == '') {
    alert("�������û���������");
    return;
}
conn.open({
    user : user,
    pwd : pass,
    appKey : 'easemob-demo#chatdemoui'//������APPKey
    //accessToken : 'YWMt8bfZfFk5EeSiAzsQ0OXu4QAAAUpoZFOMJ66ic5m2LOZRhYUsRKZWINA06HI'
});
</code></pre>

## ����{#single_chat}

### ��ѯ�����б�{#getRoster}

��ѯ�����б�ʱ��Ҫע��susciption��both��to,from��Ϊ��ֵͬ�ô���,�˴�Ĭ��both��to��Ϊ���ѣ��������Զ��崦�����ָ�APP�˴���һ�¼��ɡ�

<pre class="hll"><code class="language-javascript">
conn.**getRoster**({
    **success** : function(roster) {
        //��ȡ�����б������к����б���Ⱦ��roster��ʽΪ��
        /** [
                {
                    jid:"asemoemo#chatdemoui_test1@easemob.com",
                    name:"test1",
                    subscription: "both"
                },
                {
                    jid:"asemoemo#chatdemoui_test2@easemob.com",
                    name:"test2",
                    subscription: "from"
                }
            ]
        */
        for(var i in roster){
            var ros = roster[i];    
            //ros.subscriptioֵΪboth/toΪҪ��ʾ����ϵ��,�˴���APP�豣��һ�£����ܱ�֤�����ͻ��˵�¼��ĺ����б�һ��
            if(ros.subscription =='both' || ros.subscription=='to'){
                newroster.push(ros);
            }
        }
        if (newroster.length >=0) {
            buildContactDiv("contractlist", newroster);//ҳ�洦��
            if (newroster.length > 0) {
                setCurrentContact(newroster[0].name);//ҳ�洦����һ����ϵ����Ϊ��ǰ����div
            }
        }
        //conn.setPresence();
    },    
});
</code></pre>

### ��Ӻ���{#subscribe}
ͨ��sdk��subscribe��unsubcribe������ӻ���ɾ�����Ѳ�������¼�û�ͨ��ע��onPresence�������Է�����ӻ���ɾ���������󣬲�����Ӧ�Ĵ���
<pre class="hll"><code class="language-javascript">   
//easemobwebim-sdk���յ���ϵ�˶�������Ĵ������������typeֵ����Ӧ��ֵ��ο�xmppЭ��淶
var handlePresence = function (e){
	//��������ϣ�����Ľ����ߵĳ�ϯ��Ϣ�����������������Ϊ����
	if (e.type == 'subscribe') {
		//��e.status�к���[resp:true],���ʾΪ�Է�ͬ����Ѻ�������Լ�Ϊ���ѵ���Ϣ��demo�з��ִ�����Ϣ��Ĭ��ͬ����������˫����Ϊ���ѣ����������[resp:true]�����ʾΪ�����ĶԷ���������Լ�Ϊ���ѵ�������Ϣ��
		......
	}
	//(��������������߽������ǵĳ�ϯ��Ϣ)��������ͬ�������Ϊ����
	if (e.type == 'subscribed') {
		......
	}
	//��������ȡ��������һ��ʵ��ĳ�ϯ��Ϣ��,��ɾ�����к���
	if (e.type == 'unsubscribe') {
		.......
	}
	//�������ߵ����󱻾ܾ�����ǰ�Ķ��ı�ȡ���������Է������ɾ���˺���
	if (e.type == 'unsubscribed') {
		.......
	}
};
</code></pre>

#### ������ӶԷ�Ϊ����{#addFriend}
<pre class="hll"><code class="language-javascript">   
//����������ӶԷ�Ϊ����
var startAddFriend = function startAddFriend(){
    //�Է��û��˺�
    var user = $("addfridentId").val();
    //������ӶԷ�Ϊ����
    conn.subscribe({
		to : user,
		message : "�Ӹ�������-" + getLoacalTimeString()
	});
    return;
};
var getLoacalTimeString = function getLoacalTimeString() {
		var date = new Date();
		var time = date.getHours() + ":" + date.getMinutes() + ":"
				+ date.getSeconds();
		return time;
	}
</code></pre>

#### �Է��յ�����ͬ����߾ܾ�{#agreed_reject}

<pre class="hll"><code class="language-javascript">  
//�Է��յ������Ϊ���ѣ���������
$('#confirm-block-footer-confirmButton').click(function() {
	//ͬ���������
	agreeAddFriend(e.from);//e.from�û���
	//������ӶԷ�����
	conn.subscribe({
		to : e.from,
		message : "[resp:true]"
	});
}
//ͬ��
var agreeAddFriend = function agreeAddFriend(connection,who,jid){
   conn.subscribed({
			to : user,
			message : "[resp:true]"//ͬ����ͷ��ӶԷ�Ϊ���ѵ���Ϣ��������Ϣ��ʶ[resp:true]
		});
};

//�Է��յ������Ϊ���ѣ��ܾ�����
$('#confirm-block-footer-cancelButton').click(function() {
	rejectAddFriend(e.from);//�ܾ���Ϊ����
});
//�ܾ�
var rejectAddFriend = function(user) {
	conn.unsubscribed({
		to : user,
		message : getLoacalTimeString()
	});
};
</code></pre>

���ں��ѵķ��飬��Ӻ���ʱ��addroster����ָ��group���ԣ�Ĭ��Ϊ��default�飩����Ӻ��ѳɹ��󣬺����б���Ⱦʱ�����ݺ��ѵ�group���Խ��з�����Ⱦ��ʵ�������������칤�ߵ��Զ�����ѷ������Ĺ��ܡ�

#### ɾ������{#delfriend}

ȡ�����ģ�ͬʱ���Է����Լ��ĺ����б���ɾ������

<pre class="hll"><code class="language-javascript">
var delFriend = function(user) {
	conn.removeRoster({
		to : user,
		groups : [ 'default' ],
		success : function() {
			conn.**unsubscribed**({
				to : user
			});
		}
	});
};
</code></pre>

### �����ı������飩������Ϣ{#sendTextMessage}

<pre class="hll"><code class="language-javascript">
//�����ı���Ϣ
conn.sendTextMessage({
    to : to,//�û���¼����sd����appkey��domain��֯jid����easemob-demo#chatdemoui_**TEST**@easemob.com����"to:TEST",��ͬ
    msg :'hello world��' //�ı���Ϣ
});

//���ͱ�����Ϣ�����ýӿ�ͬ�ı���Ϣ
conn.sendTextMessage({
    to : to,
    msg :'hello world��[(*)][(#)]' //�ı���Ϣ+����
});
</code></pre>

### ����ͼƬ��Ϣ{#sendPic}

����ͼƬ��Ϣsdk�Զ���������ɣ�<br>
1���ϴ�ͼƬ�ļ��������������õ����񷵻ص�ͼƬ��Ϣ��<br>
2������ͼƬ��Ϣ����Ϣ�����ͼƬ�Ļ�����Ϣ��������·����secret�ȣ����շ���ʼ�������е�onPictureMessage�ĸ�ʽ������ͼƬ��Ϣ���ݵ�����������ͼƬ����������ʾ

<pre class="hll"><code class="language-javascript">
function sendPic() {
    //ͼƬ�����ߣ��硰test1��
    var to = curChatUserId;
    if (to == null) {
        alert("��ѡ����ϵ��");
        return;
    }
    //fileInputId���ļ�ѡ��������Id��sdk�Զ�����id�Զ���ȡ�ļ����󣨺�ͼƬ���������������ļ���
    var fileObj = Easemob.im.Helper.getFileUrl(fileInputId);
    if (fileObj.url == null || fileObj.url == '') {
        alert("��ѡ����ͼƬ");
        return;
    }
    var filetype = fileObj.filetype;
    var filename = fileObj.filename;
    if (filetype in  {
                    "jpg" : true,
                    "gif" : true,
                    "png" : true,
                    "bmp" : true
                    }) {
        var opt = {
            fileInputId : fileInputId,
            to : to,
            onFileUploadError : function(error) {
                //����ͼƬ�ϴ�ʧ��
            },
            onFileUploadComplete : function(data) {
                //����ͼƬ�ϴ��ɹ����籾����Ϣ��ʾ
            }
        };
        conn.sendPicture(opt);
        return;
    }
    alert("��֧�ִ�ͼƬ����" + filetype);
};
</code></pre>

### ������Ƶ��Ϣ{#sendAudio}

sdk����ͬ����ͼƬ��Ϣ����������

1. �ϴ���Ƶ�ļ������������õ���Ƶ�ļ�����Ϣ��
2. ������Ƶ��Ϣ�����շ�����Ϣ�������Ƶ�Ļ�����Ϣ������·����secret��Ϣ�ȣ����շ��յ���Ϣ�󣬸�����Ϣ���ڲ�����Ƶ����·����secret·����������Ƶ��������ʾ��

<pre class="hll"><code class="language-javascript">
function sendAudio () {
    var to = curChatUserId;
    if (to == null) {
        alert("��ѡ����ϵ��");
        return;
    }
    var fileObj = Easemob.im.Helper.getFileUrl(fileInputId);
    if (fileObj.url == null || fileObj.url == '') {
        alert("��ѡ������Ƶ");
        return;
    }
    var filetype = fileObj.filetype;
    var filename = fileObj.filename;
    if (filetype in {
                "mp3" : true,
                "wma" : true,
                "wav" : true,
                "avi" : true
                })
    {
        var opt = {
            fileInputId : fileInputId,
            to : to,
            onFileUploadError : function(error) {
                //�����ϴ���Ƶʧ��
            },
            onFileUploadComplete : function(data) {
                //�����ϴ���Ƶ�ɹ����籾����Ϣ��ʾ���ͳɹ�
            }
        };
        conn.sendAudio(opt);
        return;
    }
    alert("��֧�ִ���Ƶ����" + filetype);
};
</code></pre>

### ������Ϣ

#### ע�������Ϣ {#onmessage}

<pre class="hll"><code class="language-javascript">
conn.init({
	onTextMessage : function(message) {        },//�յ��ı���Ϣ������
    onEmotionMessage : function(message) {        },//�յ�������Ϣ������
    onPictureMessage : function(message) {         },//�յ�ͼƬ��Ϣ������
    onAudioMessage : function(message) {        }, //�յ�������Ϣ������
	...
});
</code></pre>

#### ������Ϣ{#options}

conn.init()��ע�᲻ͬ��Ϣ����handler֮�󣬿����н�����Ϣ�壬��λ������ѣ���׷�ӵ��������촰�ڡ�����ο�webim.easemob.comЧ������Ϣ���ʽ�μ�ǰ�½ڣ���ʼ�����ӡ�<br>
ע������ͼƬ��������Ϣ��Ҫ�Ƚ������أ�Ȼ�������ʾ���߲��Ŵ�������(����ͼƬ����Ƶͬ)��
<pre class="hll"><code class="language-javascript">
var handlePictureMessage = function(message) {
var filename = message.filename;//�ļ����ƣ����ļ���չ��
var from = message.from;//�ļ��ķ�����
var mestype = message.type;//��Ϣ���͵�������Ⱥ����Ϣ���Ǹ�����Ϣ
......
...
var options = message;
// ͼƬ��Ϣ���سɹ���Ĵ����߼�
options.onFileDownloadComplete = function(response, xhr) {
	var objectURL = window.URL.createObjectURL(response);
	img = document.createElement("img");
	img.onload = function(e) {
		img.onload = null;
		window.URL.revokeObjectURL(img.src);
	};
	img.onerror = function() {
		img.onerror = null;
		if (typeof FileReader == 'undefined') {
			img.alter = "��ǰ�������֧��blob��ʽ";
			return;
		}
		img.onerror = function() {
			img.alter = "��ǰ�������֧��blob��ʽ";
		};
		var reader = new FileReader();
		reader.onload = function(event) {
			img.src = this.result;
		};
		reader.readAsDataURL(response);
	}
	img.src = objectURL;
	var pic_real_width = options.width;
	......
	...
};
options.onFileDownloadError = function(e) {
	appendMsg(from, contactDivId, e.msg + ",����ͼƬ" + filename + "ʧ��");
};
**Easemob.im.Helper.download(options)**;

</code></pre>

#### ��ʷ��Ϣ{#history_message}

sdk�ݲ����л�����ʷ��Ϣ���ܣ�demo�����촰��ֻ����ʾ����ǰ��¼��Ựʵʱ��������Ϣ�����ܲ鿴��ʷ��Ϣ�����ԶԵ�¼���������Ϣ�������������

#### ����Ϣ��ʾ{#new_message}

sdk���յ�����Ϣ�ǻ�ֱ��ת������¼�û������յ���Ϣ��demo�л��ں��ѻ���Ⱥ��ĺ�����ʾ��ɫ��Ϣ����������ʽ�����߿����д���

## Ⱥ��{#group_chat}

### ��ѯȺ���Ա{#queryOccupants}

<pre class="hll"><code class="language-javascript">
//����roomId��ѯroom��Ա�б�
var queryOccupants = function queryOccupants(roomId) {
    var occupants = [];//��ų�Ա����
    //��ѯ��ȡroom��Ϣ
    conn.queryRoomInfo({
        roomId : roomId,
        success : function(occs) {
            if (occs) {
                for ( var i = 0; i < occs.length; i++) {
                    occupants.push(occs[i]);
                }
            }
            //��ѯ��ȡroom��Ա��Ϣ
            conn.queryRoomMember({
                roomId : roomId,
                success : function(members) {
                    if (members) {
                        for ( var i = 0; i < members.length; i++) {
                            occupants.push(members[i]);
                        }
                    }
                }
            });
        }
    });
};
</code></pre>

### �����ı������飩������Ϣ{#group_sendTextMessage}

<pre class="hll"><code class="language-javascript">
//�����ı���Ϣ
conn.sendTextMessage({
    to : to,
    type : 'groupchat',
    msg :'hello world��' //�ı���Ϣ
});

//���ͱ�����Ϣ�����ýӿ�ͬ�ı���Ϣ
conn.sendTextMessage({
    to : to,
    type : 'groupchat',
    msg :'hello world��[(*)][(#)]' //�ı���Ϣ+����
});
</code></pre>

### ����ͼƬ��Ϣ{#group_sendPic}

����ͼƬ��Ϣsdk�Զ����������

1. �ϴ�ͼƬ�ļ�
2. ����ͼƬ��Ϣ��ʼ�������е�onPictureMessage�ĸ�ʽ

<pre class="hll"><code class="language-javascript">
//����ͼƬ��Ϣʱ���÷���
var sendPic = function() {
    var to = curChatUserId;
    if (to == null) {
        return;
    }
    // Easemob.im.Helper.getFileUrlΪeasemobwebim-sdk��ȡ�����ļ�����ķ�����fileInputIdΪ input ��ǩ��idֵ
    var fileObj = Easemob.im.Helper.getFileUrl(fileInputId);
    if (fileObj.url == null || fileObj.url == '') {
        alert("��ѡ����ͼƬ");
        return;
    }
    var filetype = fileObj.filetype;
    var filename = fileObj.filename;
    if (filetype in pictype) {
        document.getElementById("fileSend").disabled = true;
        document.getElementById("cancelfileSend").disabled = true;
        var opt = {
            type:'chat',
            fileInputId : fileInputId,
            to : to,
            onFileUploadError : function(error) {
                //����ͼƬ�ϴ�ʧ��
            },
            onFileUploadComplete : function(data) {
                //�ر��ļ�ѡ�񴰿�
                $('#fileModal').modal('hide');
                //��������ͼ
                var file = document.getElementById(fileInputId);
                if (file && file.files) {
                    var objUrl = getObjectURL(file.files[0]);
                    if (objUrl) {
                        var img = document.createElement("img");
                        img.src = objUrl;
                        img.width = maxWidth;
                    }
                }
            
            }
        };
        //�ж��Ƿ�ΪȺ���ʶ
        if (curChatUserId.indexOf(groupFlagMark) >= 0) {
            opt.type = 'groupchat';//Ⱥ���ʶ��
            opt.to = curRoomId;
        }
        conn.sendPicture(opt);
        return;
    }
    alert("��֧�ִ�ͼƬ����" + filetype);
};
</code></pre>

### ������Ƶ��Ϣ{#group_sendAudio}

sdk����ͬȺ����ͼƬ��Ϣ��������

1. �ϴ���Ƶ
2. ������Ϣ

<pre class="hll"><code class="language-javascript">
//������Ƶ��Ϣʱ���õķ���
var sendAudio = function() {
    var to = curChatUserId;
    if (to == null) {
        alert("��ѡ����ϵ��");
        return;
    }
    //����easemobwebim-sdk�ṩ�ķ���������һ��file����
    var fileObj = Easemob.im.Helper.getFileUrl(fileInputId);
    if (fileObj.url == null || fileObj.url == '') {
            alert("��ѡ������Ƶ");
        return;
    }
    var filetype = fileObj.filetype;
    var filename = fileObj.filename;
    if (filetype in audtype) {
        document.getElementById("fileSend").disabled = true;
        document.getElementById("cancelfileSend").disabled = true;
        var opt = {
            type:"chat",
            fileInputId : fileInputId,
            to : to,//����˭
            onFileUploadError : function(error) {
                //�����ϴ���Ƶʧ��
            },
            onFileUploadComplete : function(data) {
                //�����ϴ���Ƶ�ɹ����籾����Ϣ��ʾ���ͳɹ�
            }
        };
        //������opt��������easemobwebim-sdk�з�����Ƶ�ķ���
        if (curChatUserId.indexOf(groupFlagMark) >= 0) {
            opt.type = 'groupchat';
            opt.to = curRoomId;
        }
        conn.sendAudio(opt);
        return;
    }
    alert("��֧�ִ���Ƶ����" + filetype);
};
</code></pre>
### ���ռ�������Ϣ{#messageType}
Ⱥ�Ľ��ռ�������Ϣͬ���ģ���Ϣ���뵥����Ϣ����message��type�������֣�����Ϊ����chat����Ⱥ��Ϊ����groupchat����������Ϣ�����ͽ��в�ͬ�����ɡ�

## �˳�{#quit}

### �ر�����{#conn_close}
//sdk�ر����Ӳ���������״̬ΪCLOSED
<pre class="hll"><code class="language-javascript">
conn.close();
</code></pre>

## ������˵��{#sdk_tools}

### ���鹤����{#emotion}

<pre class="hll"><code class="language-javascript">
//���ر���JSON object����ʽΪ��
    {
        "[):]" : "data:image/png;base64,iVBORw0K....==",
        "[:D]" : "data:image/png;base64,iVBORw0KGgoAAAANSUh....=="
    }

var emotion_json = Easemob.im.Helper.EmotionPicData;
</code></pre>

### Base64������{#base64}

<pre class="hll"><code class="language-javascript">
var base64  = Easemob.im.Helper.Base64;
var srcstr="ssss";
var base64str = base64.encode(srcstr);
var orgstr = base64.decode(srcstr);
</code></pre>

### �ļ��ϴ�������{#fileupload}

<pre class="hll"><code class="language-javascript">
//�Ƿ����ϴ�file
var canupload = Easemob.im.Helper.isCanUploadFile;
//�Ƿ�������file
var candownload = Easemob.im.Helper.isCanDownLoadFile ;
//�Ƿ�����header
var hasheader = Easemob.im.Helper.hasSetRequestHeader;
//�Ƿ�����mimetype
var hasmimetype = Easemob.im.Helper.hasOverrideMimeType;
</code></pre>

### �������������{#handleMotion}

<pre class="hll"><code class="language-javascript">
//���ر���JSON����ʽΪ��
{
    isemotion:true;
    body:[{
        type:txt,
        msg:ssss
    },
    {
        type:emotion,
        msg:imgdata
    }]
}

var emotionMsg = Easemob.im.Helper.parseTextMessage(message);
</code></pre>

### �ļ��ϴ�������{#fileupdate}

<pre class="hll"><code class="language-javascript">
//����fileinfo���󣬸�ʽΪ��
    {
        url : '',
        filename : '',
        filetype : ''
    }
var fileInfo = Easemob.im.Helper.getFileUrl(fileInputId);
//�ϴ�
var options={
    appName = 'chatdemoui',
    orgName = 'easemob-demo',
    accessToken = 'YWMtjPPoovCqEeOQs7myPqqaOwAAAUaqNH0a8rRj4PwJLQju6-S47ZO6wYs3Lwo',
    onFileUploadComplete:function(data){//upload file success },
    onFileUploadError:function(e){//upload file error },
    width:100,//only for pic
    heght:100//only for pic
}
Easemob.im.Helper.upload(options);
//����
var options = {
    method:'GET',//default GET
    responseType:'blob',//default blob
    mimeType:'text/plain; charset=x-user-defined',//default
    url:'http://s1.easemob.com/weiquan2/a2/chatfiles/0c0f5f3a-e66b-11e3-8863-f1c202c2b3ae',
    secret = 'NSgGYPCxEeOou00jZasg9e-GqKUZGdph96EFxJ4WxW-qkxV4',
    accessToken = 'YWMtjPPoovCqEeOQs7myPqqaOwAAAUaqNH0a8rRj4PwJLQju6-S47ZO6wYs3Lwo',
    onFileUploadComplete:function(data){//upload file success },
    onFileUploadError:function(e){//upload file error },
}
Easemob.im.Helper.download(options);
//�ļ���С 
var options={
    fileInputId:'uploadfileinput'//�ļ������id
};
var fileSize = getFileSize(options.fileInputId);;
</code></pre>

### ����Ajax����{#ajaxresquest}

<pre class="hll"><code class="language-javascript">
var options = {
    dataType:'text',//default
    success:function(){//handle request success},
    error :function(){//handle request error},
    type : 'post',//default 'post'
    url : 'http://s1.easemob.com/weiquan2/a2/chatfiles/0c0f5f3a-e66b-11e3-8863-f1c202c2b3ae',
    headers:'',//default {}
    data : '';//default null
};
Easemob.im.Helper.xhr(options);
</code></pre>

### ��¼{#sdk_login}

<pre class="hll"><code class="language-javascript">
var options = {
    appKey:'easemob-demo#chatdemoui',//default ''
    success:function(data){ //login success },//default emptyFn
    error : cunction(error){ //login error }, //default emptyFn
    user : 'test1', //default ''
    pwd : '123456'  //default ''
};
Easemob.im.Helper.login2UserGrid(options);
</code></pre>

### ���ÿպ���{#null_function}

��������Ҫ�ص��ĵط����ܵ�����ʱ��Ĭ�ϲ��ô˺���

<pre class="hll"><code class="language-javascript">
var emptyFn = function() {};
</code></pre>
