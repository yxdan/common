# common
常用js 封装
js中常用的方法封装

const utils = {
    // 20160817-->2016年08月17日
    formatDate: (value) => {
        if (value) {
            return value.slice(4, 6) + "月" + value.slice(6, 8) + "日";
        }
    },
    /**两个时间差：天*/
    DateDiff: (checkTime1, checkTime2) => {
        return Math.floor((checkTime1 - checkTime2) / (24 * 60 * 60 * 1000));
    },
    // 格式化数据
    formatData: (value, fixed, unit) => {
        if (!!value || value === 0) {
            if (fixed || isFinite(fixed)) {
                if (unit) {
                    return value.toFixed(fixed) + unit;
                } else {
                    return value.toFixed(fixed);
                }
            } else {
                if (unit) {
                    return value + unit;
                } else {
                    return value;
                }
            }
        } else {
            return '--'
        }
    },
    setLocalStorage: (key, val) => {
        window.localStorage.setItem(key, val);
    },
    getLocalStorage: (key) => {
        window.localStorage.getItem(key);
    },
    isBrowser: () => {
        var flag = 'android';
        var ua = window.navigator.userAgent.toLowerCase();
        if (ua.match(/MicroMessenger/i) == 'micromessenger') { //是微信
            console.log(1)
            if(/(?:android)/.test(ua)){
                console.log('Android');
                flag = 'android';
            }else{
                console.log('iphone');
                flag = 'iphone';
            } //ios终端
        } else {
            console.log(2)
        }
        return flag;
    },
    // 获取url中的参数
    getUrlParam: (name) => {
        var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
        var r = window.location.search.substr(1).match(reg);
        if (r != null) {
            return unescape(r[2]);
        } else {
            return null;
        }
    },
    // 获取ios url中的参数
    getIOSUrlParam: (name) => {
        var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
        var r = window.location.search.substr(1).match(reg);
        if (r != null) {
            return r[2];
        } else {
            return null;
        }
    },
    // 设置cookie
    addCookie: (name, value, expiresHours) => {
        var date = new Date();
        expiresHours = expiresHours | 24 * 30;
        if (expiresHours > 0) {
            date.setTime(date.getTime() + expiresHours * 3600 * 1000);
            document.cookie = name + "=" + value + ";expires=" + date.toGMTString() + ";path=/";
        }

    },
    // 获取cookie
    getCookie: (name) => {
        var strCookie = document.cookie;
        var arrCookie = strCookie.split(";");
        for (var i = 0; i < arrCookie.length; i++) {
            var arr = arrCookie[i].split("=");
            if (arr[0].replace(/(^\s*)|(\s*$)/g, "") == name) {
                return arr[1];
            }
        }
        return "";
    },
    // 删除cookie
    deleteCookie: (name) => {
        var date = new Date();
        date.setTime(date.getTime() - 10000);
        document.cookie = name + "=v; expires=" + date.toGMTString() + ";path=/";
    },
    /**时间戳转为yyyy-mm-dd*/
    getNowtime: (data, detail) => {
        if (!data) {
            return "";
        }
        var date = new Date(data);
        var year = date.getFullYear();
        var month = date.getMonth() + 1;
        month = month < 10 ? ("0" + month) : month;
        var day = date.getDate();
        day = day < 10 ? ("0" + day) : day;
        var ymd = year + "-" + month + "-" + day;
        if (!detail) {
            return ymd;
        }
        var hour = date.getHours();
        hour = hour < 10 ? ("0" + hour) : hour;
        var minu = date.getMinutes();
        minu = minu < 10 ? ("0" + minu) : minu;
        var second = date.getSeconds();
        second = second < 10 ? ("0" + second) : second;
        return ymd + " " + hour + ":" + minu + ":" + second;
    },
    /**时间戳转为yyyy-mm-dd...*/
    getFormatTime: (data, detail) => {
        if (!data) {
            return "";
        }
        if (_.isString(data)) {
            data = data.replace(/-/g, '/');
        }
        var date = new Date(data);
        var year = date.getFullYear();
        var month = date.getMonth() + 1;
        month = month < 10 ? ("0" + month) : month;
        var day = date.getDate();
        day = day < 10 ? ("0" + day) : day;
        var ymd = year + "-" + month + "-" + day;

        var hour = date.getHours();
        hour = hour < 10 ? ("0" + hour) : hour;
        var minu = date.getMinutes();
        minu = minu < 10 ? ("0" + minu) : minu;
        var second = date.getSeconds();
        second = second < 10 ? ("0" + second) : second;

        var xqValue = date.getDay();
        var xq = '';
        if (xqValue == 0) {
            xq = "周日";
        } else if (xqValue == 1) {
            xq = "周一";
        } else if (xqValue == 2) {
            xq = "周二";
        } else if (xqValue == 3) {
            xq = "周三";
        } else if (xqValue == 4) {
            xq = "周四";
        } else if (xqValue == 5) {
            xq = "周五";
        } else if (xqValue == 6) {
            xq = "周六";
        }
        if (detail == "md") {
            return month + "月" + day + "日";
        }
        if (detail == "m-d") {
            return month + "-" + day;
        }
        if (detail == "xq") {
            return xq;
        }
        if (detail == "hms") {
            return hour + ":" + minu + ":" + second;
        }
        if (detail == "hm") {
            return hour + ":" + minu;
        }
        if (detail == "mdhm") {
            return month + "-" + day + " " + hour + ":" + minu;
        }
        if (detail == "ymdhms") {
            return ymd + " " + hour + ":" + minu + ":" + second;
        }
        if (detail == "ymd") {
            return ymd;
        }
        if (detail == "ymdhm") {
            return year + '/' + month + '/' + day + ' ' + hour + ':' + minu;
        }
        if (detail == "dateStr") {
            return year + '' + month + day;
        }
        if (detail == "zdzb_time") {
            return year + '' + month + day + '-060101-223-8';
        }
        if (detail == "ymd/") {
            return month + '/' + day + '/' + year;
        }
        if (detail == "ymd/hm") {
            return month + '/' + day + '/' + year + ' ' + hour + ':' + minu;
        }
        if (detail == "md/hm") {
            return month + '/' + day + ' ' + hour + ':' + minu;
        }
        if (detail == "y/m/d") {
            return year + '/' + month + '/' + day;
        }
        if (detail == "y-m-d") {
            return year + '-' + month + '-' + day;
        }
        if (detail == "m/d") {
            return month + '/' + day;
        }
        if (detail == "y/m/d/hm") {
            return year + '/' + month + '/' + day + ' ' + hour + ":" + minu;
        }
        if (detail == "y.m") {
            return year + '.' + month;
        }
        if (detail == "m") {
            return month;
        }
        if (detail == "d") {
            return day;
        }
        if (detail == "md-hm") {
            return month + "月" + day + "日 " + hour + ":" + minu;
        }
    },
    // 获取用户信息
    getUserInfo: (uid) => {
        // const current = AV.User.currentUser();
        if (uid) {
            var args = {
                user_id: String(uid)
            }
            return api.qkz_user.getInfo(args);
        } else if (!utils.getCookie("uid")) {
            let promise = $.Deferred();
            promise.reject("数据错误")
            return promise;
        } else {
            var args = {
                user_id: String(utils.getCookie("uid"))
            }
            return api.qkz_user.getInfo(args);
        }
    },
    // 获取错误提示框
    getPopup: (msg, btnText, callback) => {
        btnText = btnText || '确定'
        var str = '<div class="popup_main" id="popup_test" style="display:block">' +
                '<div class="mui-popup mui-popup-in ">' +
                    '<div class="mui-popup-inner">' +
                        '<div class="mui-icon mui-icon-closeempty" id="popup_close"></div>' +
                        '<div class="popup_title">提醒信息</div>' +
                        '<div class="popup_list">' +
                            '<p class="info">' + msg + '</p> ' +
                        '</div> ' +
                    '</div>' +
                    '<div class="popup-buttons"> ' +
                        '<button class="mui-btn mui-btn-primary mui-btn-block red_btn" id="close_popup">' + btnText + '</button> ' +
                    '</div> ' +
                '</div>' +
                '<div class="mui-popup-backdrop mui-active"></div>' +
            '</div>';        
        var dom = $(str);
        dom.find('#popup_close').click(function() {
            dom.remove();
        });
        dom.find('#close_popup').click(function() {
            if(callback){
                callback();
            }
            dom.remove();
        });
        $(".mui-content").append(dom);
    },
    // 获取loading界面
    getLoading: () => {
        var str = '<div class="popup_load">' +
            '<div class="mui-popup mui-popup-in ">' +
            '<div class="load_icon"></div>' +
            '</div>' +
            '<div class="mui-popup-backdrop no-bg mui-active"></div>' +
            '</div>';
        $(".mui-content").append(str);
    },
    // 隐藏loading界面
    hideLoading: () => {
        if ($(".popup_load").length > 0) {
            $(".popup_load").remove();
        }
    },
    nl2br: (str, is_xhtml) => {
        var breakTag = (is_xhtml || typeof is_xhtml === 'undefined') ? '<br />' : '<br>';
        return (str + '').replace(/([^>\r\n]?)(\r\n|\n\r|\r|\n)/g, '$1' + breakTag + '$2');
    },
    getUrlArgs: () => {
        let url = window.location.href,
            urlArr = url.split("?"),
            json = {};
        if (urlArr[1]) {
            var args = urlArr[1].split("&");
            for (var i = 0; i < args.length; i++) {
                var tmpArr = args[i].split("=");
                json[tmpArr[0]] = tmpArr[1];
            }
        }
        return json;
    },
    //将 window.location.href 改为 window.location.search
    getUrlArgs2: () => {
        let url = window.location.search,
            urlArr = url.split("?"),
            json = {};
        if (urlArr[1]) {
            var args = urlArr[1].split("&");
            for (var i = 0; i < args.length; i++) {
                var tmpArr = args[i].split("=");
                json[tmpArr[0]] = tmpArr[1];
            }
        }
        return json;
    },
    getDateString: (date) => {
        console.log(date);
        let diff = new Date() - new Date(date),
            string = '';
        if (diff < 1000 * 60 * 60) {
            string = "刚刚";
        } else if (diff < 1000 * 60 * 60 * 24) {
            //小时
            string = Math.floor((diff / (1000 * 60 * 60))) + "小时前";
        } else if (diff < 1000 * 60 * 60 * 24 * 30) {
            //天
            string = Math.floor((diff / (1000 * 60 * 60 * 24))) + "天前";
        } else if (diff < 1000 * 60 * 60 * 24 * 30 * 12) {
            //月
            string = Math.floor((diff / (1000 * 60 * 60 * 24 * 30))) + "月前";
        } else {
            //年
            string = Math.floor((diff / (1000 * 60 * 60 * 24 * 30 * 12))) + "年前";
        }
        // console.log(string)
        return string
    },
    getDayString: (date) => {
        let diff = new Date() - new Date(date),
            string = '';
        if (diff < 1000 * 60 * 60 * 24) {
            string = "1";
        } else {
            string = Math.floor((diff / (1000 * 60 * 60 * 24)));
        }
        return string
    },
    postHandleData: (result) => {
        if (_.isArray(result)) {
            let newResult = [];
            $.each(result, function(i, result) {
                let temp = {},
                    attributes = result.attributes,
                    objectId = { id: result.id },
                    updatedAt = { updatedAt: result.updatedAt },
                    createdAt = { createdAt: result.createdAt };
                _.extend(temp, objectId, updatedAt, createdAt, attributes);
                newResult.push(temp);
            });
            return newResult
        } else {
            let temp = {},
                attributes = result.attributes,
                objectId = { id: result.id },
                updatedAt = { updatedAt: result.updatedAt },
                createdAt = { createdAt: result.createdAt };
            _.extend(temp, attributes, objectId, updatedAt, createdAt);
            return temp
        }
    },
    //只显示几行字符串
    getFilterString: (str, rows) => {
        var dWidth = $(document).width();
        var length = Math.ceil(dWidth / 14) * rows;
        return [str.substring(0, length), str.length > length];
    },
    filterString: (str, rows, num) => {
        var dWidth = $(document).width() - num;
        var length = Math.ceil(dWidth / 14) * rows;
        return [str.substring(0, length), str.length > length];
    },
    //单位换算
    getFormatUnit: (num) => {
        if (!_.isNumber(num) || isNaN(num)) {
            return 0;
        }
        if (num > 10000 * 10000) {
            return (num / (10000 * 10000)).toFixed(2) + '亿';
        } else if (num > 10000) {
            return (num / 10000).toFixed(2) + '万';
        } else {
            return num;
        }
    },
    // 获取股票信息
    getStockInformation: (args, parmas, name, length_count, names) => {
        api.get(args, parmas).done(function(data) {
            var result = data.Data.RepDataJianPanBaoShuChu[0].JieGuo[0].ShuJu || '';
            var str = '';
            jQuery.each(result, function(i, val) {
                if (val.ShuXing != '上证指数' && val.ShuXing != '深证指数') {
                    str += '<li data-id="' + val.DaiMa + '"><span class="status">' + val.ShuXing + '</span><span class="name">' + val.MingCheng + '</span><span class="code">' + val.DaiMa + '</li>';
                }
                length_count++;
            });
            if (length_count < 5) {
                $(names).css("height", (length_count * 36) + "px")
            }
            $(name).html(str);
        });
    },
    goToProdCent: (authid) => {
        location.href = `/goToProdCent?authid=${authid}`;
    },
    // 获取免责声明: 1(智能产品),2(人工产品),3(掘金、直播、学堂)
    getDisclaimer: (type) => {
        var str = '';
        if (type == 1) {
            str = '<div class="popup_main" id="disclaimer_main" style="display:block">' +
                '<div class="mui-popup mui-popup-in ">' +
                '<div class="mui-popup-inner">' +
                '<div class="mui-icon mui-icon-closeempty" id="disclaimer_close"></div>' +
                '<div class="popup_list">' +
                '<dl class="disclaimer_list">' +
                '<dt>1、数据来源</dt>' +
                '<dd>数据来源含沪深交易所披露公开信息、上市公司公告、各大财经媒体及中证、上证、证券时报，部分来源自钱坤投资大数据中心的海量数据等，仅供参考。</dd>' +
                '<dt>2、风险提示</dt>' +
                '<dd>本产品有投资风险，我司不以任何方式向投资者做出不受损失或者取得最低收益的承诺。投资者应当自主做出投资决策，并自行承担投资风险。</dd>' +
                '<dt>3、免责声明</dt>' +
                '<dd>本产品所依据的信息、数据资讯仅供参考，我司对这些信息的准确性及完整性不做任何保证。投资者依据产品信息进行投资决策所产生的收益和损失，与我司无关，我司不承担任何法律责任。</dd>' +
                '<dt>4、版权说明</dt>' +
                '<dd>信息版权归我司所有，未经本公司事先书面认可，任何机构和个人不得以任何形式翻版、复制、引用或转载。否则，本公司将保留随时追究其法律责任的权利。</dd>' +
                '</dl>' +
                '</div>' +
                '</div>' +
                '</div>' +
                '<div class="mui-popup-backdrop mui-active"></div>' +
                '</div>';
        } else if (type == 2) {
            str = '<div class="popup_main" id="disclaimer_main" style="display:block">' +
                '<div class="mui-popup mui-popup-in ">' +
                '<div class="mui-popup-inner">' +
                '<div class="mui-icon mui-icon-closeempty" id="disclaimer_close"></div>' +
                '<div class="popup_list">' +
                '<dl class="disclaimer_list">' +
                '<dt>1、数据来源</dt>' +
                '<dd>数据来源含沪深交易所披露公开信息、上市公司公告、各大财经媒体及中证、上证、证券时报，部分来源自钱坤投资大数据中心的海量数据等，仅供参考。</dd>' +
                '<dt>2、风险提示</dt>' +
                '<dd>本产品有投资风险，我司不以任何方式向投资者做出不受损失或者取得最低收益的承诺。投资者应当自主做出投资决策，并自行承担投资风险。</dd>' +
                '<dt>3、免责声明</dt>' +
                '<dd>本产品所依据的信息、数据资讯仅供参考，我司对这些信息的准确性及完整性不做任何保证。投资者依据产品信息进行投资决策所产生的收益和损失，与我司无关，我司不承担任何法律责任。</dd>' +
                '<dt>4、版权说明</dt>' +
                '<dd>信息版权归我司所有，未经本公司事先书面认可，任何机构和个人不得以任何形式翻版、复制、引用或转载。否则，本公司将保留随时追究其法律责任的权利。</dd>' +
                '</dl>' +
                '</div>' +
                '</div>' +
                '</div>' +
                '<div class="mui-popup-backdrop mui-active"></div>' +
                '</div>';
        } else if (type == 3) {
            str = '<div class="popup_main" id="disclaimer_main" style="display:block">' +
                '<div class="mui-popup mui-popup-in ">' +
                '<div class="mui-popup-inner">' +
                '<div class="mui-icon mui-icon-closeempty" id="disclaimer_close"></div>' +
                '<div class="popup_list">' +
                '<dl class="disclaimer_list">' +
                '<dt>1、数据来源</dt>' +
                '<dd>数据来源含沪深交易所披露公开信息、上市公司公告、各大财经媒体及中证、上证、证券时报，部分来源自钱坤投资大数据中心的海量数据等，仅供参考。</dd>' +
                '<dt>2、风险提示</dt>' +
                '<dd>本产品有投资风险，我司不以任何方式向投资者做出不受损失或者取得最低收益的承诺。投资者应当自主做出投资决策，并自行承担投资风险。</dd>' +
                '<dt>3、免责声明</dt>' +
                '<dd>本产品所依据的信息、数据资讯仅供参考，我司对这些信息的准确性及完整性不做任何保证。投资者依据产品信息进行投资决策所产生的收益和损失，与我司无关，我司不承担任何法律责任。</dd>' +
                '<dt>4、版权说明</dt>' +
                '<dd>信息版权归我司所有，未经本公司事先书面认可，任何机构和个人不得以任何形式翻版、复制、引用或转载。否则，本公司将保留随时追究其法律责任的权利。</dd>' +
                '</dl>' +
                '</div>' +
                '</div>' +
                '</div>' +
                '<div class="mui-popup-backdrop mui-active"></div>' +
                '</div>';
        } else if (type == 4) {
            str = '<div class="popup_main" id="disclaimer_main" style="display:block">' +
                '<div class="mui-popup mui-popup-in ">' +
                '<div class="mui-popup-inner">' +
                '<div class="mui-icon mui-icon-closeempty" id="disclaimer_close"></div>' +
                '<div class="popup_list">' +
                '<dl class="disclaimer_list gold_disclaimer_list">' +
                '<dt>通用产品的免责声明</dt>' +
                '<dd>本产品提供的证券咨询和投资顾问相关的内容主要包括：研究报告，实时解盘，依据技术指标的交易系统和选股模型，依据数据模型的选股方法等。并通过产品的文字，指标，交易系统，选股结果，股票池等方式显示。 本产品提供的买入、卖出建议，提供的股票池和投资建议，仅供投资者参考，投资者基于独立的判断，自行决定证券投资，并承担投资损失。</dd>' +
                '<dt>含有研究报告摘要产品免责条款</dt>' +
                '<dd>本报告的信息来源于已公开的资料，本公司对该等信息的准确性、完整性或可靠性不作任何保证。本报告所载的资料、意见及推测仅反映本公司于发布本报告当日的判断，本报告所指的证券或投资标的的价格、价值及投资收入可升可跌。过往表现不应作为日后的表现依据。在不同时期，本公司可发出与本报告所载资料、意见及推测不一致的报告。本公司不保证本报告所含信息保持在最新状态。同时，本公司对本报告所含信息可在不发出通知的情形下做出修改，投资者应当自行关注相应的更新或修改。本报告中所指的投资及服务可能不适合个别客户，不构成客户私人咨询建议。在任何情况下，本报告中的信息或所表述的意见均不构成对任何人的投资建议。在任何情况下，本公司、本公司员工或者关联机构不承诺投资者一定获利，不与投资者分享投资收益，也不对任何人因使用本报告中的任何内容所引致的任何损失负任何责任。投资者务必注意，其据此做出的任何投资决策与本公司、本公司员工或者关联机构无关。</dd>' +
                '<dt>资讯产品的免责条款</dt>' +
                '<dd>以上信息仅供参考，不作为投资依据。信息内容根据行业通行的准则，以合法渠道获得，尽可能保证可靠、准确和完整，但并不保证所述信息的准确性和完整性。不能作为道义的、责任的和法律的依据或者凭证，无论是否已经明示或者暗示。</dd>' +
                '</dl>' +
                '</div>' +
                '</div>' +
                '</div>' +
                '<div class="mui-popup-backdrop mui-active"></div>' +
                '</div>';
        }
        var dom = $(str);
        dom.find('#disclaimer_close').click(function() {
            dom.remove();
        });
        $(".mui-content").append(dom);
    },
    dealUrlStr: (url, str) => {
        if (/\?/.test(url)) {
            return url + '&' + str;
        } else {
            return url + '?' + str;
        }
    },
    getStrDate: (str) => {
        return str.replace(/(\d{4})(\d{2})(\d{2})/, '$1-$2-$3')
    },
    // 原生登陆
    appLogin: () => {
        location.href = "http://wwww.baidu.com?code=111#dzqkLogin";
    },
    // 原生跳转我的组合
    appZuHe: () => {
        location.href = "http://wwww.baidu.com#dzqkProfolio";
    },
    // 原生跳转我的策略
    appStrategy: () => {
        location.href = "http://wwww.baidu.com#dzqkStockPool"
    },
    appCloseWeb: () => {
        location.href = "http://wwww.baidu.com#dzqkCloseWeb"
    },
    // 获取用户特权状态
    getUserPrivilege: (authId) => {
        if (authId) {
            var args = {
                auth_id: authId
            };
            return api.javaAjax2('api/v2/user/is_privilege',args,'get', true);
        }
    },    
    // 产品编号存本地
    setProCode: () => {
        let args = {};
        api.javaAjax2('api/v2/user/options',args,'get').done((data) => {
            // console.log("产品编号",data.data);
            if (data.code == 0) {
                localStorage.setItem("productCode",JSON.stringify(data.data));
            }
        }).fail((msg) => {
            console.log(msg);
        })
    },
    // 自动隐藏框
    autoHidePopup: (value) => {
        let info = value || '订阅成功，最新资讯会第一时间推送！';
        mui.alert(info);
        // let str = '';
        //     str = '<div class="popup_main autoHidePopup" id="autoHidePopup" style="display:block">' +
        //         '<div class="mui-popup mui-popup-in ">' +
        //         '<div class="mui-popup-inner">' +
        //         '<div class="mui-icon mui-icon-closeempty" id="autoHidePopup_close"></div>' +
        //         '<div class="popup_list">' + info +
        //         '</div>' +
        //         '</div>' +
        //         '</div>' +
        //         '<div class="mui-popup-backdrop mui-active"></div>' +
        //         '</div>';        
        // let dom = $(str);
        // dom.find('#autoHidePopup_close').click(function() {
        //     dom.remove();
        // });
        // $(".mui-content").append(dom);
        // setTimeout(function() {
        //     dom.remove();
        // }, 2000);
    },
    /**
    * 记录用户行为
    * @param {action_key} 用户行为key
    */
    getAction: (action_key,src) => {
        let args = {
            action_key: action_key,
            action: src,
            remark: ""
        };
        api.javaAjax2('api/v2/user/action', args, "POST").done((data) => {
            if (data.code == 0) {
            }
        }).fail((msg) => {
            console.log(msg);
        });
    },
    go_page(url) {
        mui.openWindow({
            id: url,
            url: url,
            show: {
                aniShow: 'slide-in-right',
                duration: 300
            }
        })
    }
}


export default utils;
