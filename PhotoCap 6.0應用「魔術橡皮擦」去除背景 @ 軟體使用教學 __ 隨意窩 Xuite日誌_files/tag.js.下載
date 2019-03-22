(function(t) {
    function setCookie(name,value,days) {
        var expires = '';
        if (days) {
            var date = new Date();
            date.setTime(date.getTime() + (days*24*60*60*1000));
            expires = '; expires=' + date.toUTCString();
        }
        document.cookie = name + '=' + value + expires + '; path=/';
    }
    function readCookie(name) {
        var nameEQ = name + '=';
        var ca = document.cookie.split(';');
        for(var i=0;i < ca.length;i++) {
            var c = ca[i];
            while (c.charAt(0)==' ') c = c.substring(1,c.length);
            if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
        }
        return null;
    }
    var ht = function ht() {
        var tid = readCookie('uuid');
        return {
            fire: function fire(opt, callback){
                if(opt) {opt = '&t=' + encodeURIComponent(opt);} else {opt = '';}
                if(!tid){
                    var r = new XMLHttpRequest();
                    r.open('GET', '//' + t + '/index.php', true);
                    r.withCredentials=true;
                    r.onreadystatechange = function () {
                        if (r.readyState != 4 || r.status != 200) return;
                        tid = r.responseText;
                        if (tid.length === 64 || tid.length === 32 || tid.length === 36) {
                            setCookie('uuid',tid,365*2);
                            var trackingImage = new Image();
                            trackingImage.src = '//' + t + '/pixel?bd='+tid + opt;
                            if (callback) { callback(tid); }
                        }
                    };
                    r.send();
                }else{
                    var trackingImage = new Image();
                    trackingImage.src = '//' + t + '/pixel?bd='+tid + opt;
                    if (callback) { callback(tid); }
                }
            }
        }
    }
    window.hitag = new ht();
    var tagDom = document.getElementsByTagName('hitag')[0];
    if (tagDom) {
        var tag = (tagDom.dataset && tagDom.dataset.tag) ? tagDom.dataset.tag: '';
        if (tag !== '') {hitag.fire(tag)} 
	else {hitag.fire()}
    }
})('t.ssp.hinet.net');
