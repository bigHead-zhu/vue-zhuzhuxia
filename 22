<template>
	<div class="date-main">
		<div class="header">
			<!--<img class="icon-left" src="../../../static/img/icon-left-blod.png"/>-->
			<label class="header-title">选择日期</label>
			<span class="ok-btn">完成</span>
		</div>
		<ul class="week-title">
			<li class="c1e f28" v-for="(item,index) in week" :key="index">{{item}}</li>
		</ul>
		<div class="main">
			<!-- 内容 -->
			<div class="table">
				<div 
					v-for="(item, index) in days"
					:key="index"
					class="mouth">
					<div class="mouth-title">
						{{ item.dateTile }}
					</div>
					<ul class="date-table clear">
						<li  class="f28  "  v-for="(dayobject,indexo) in item.dayArr" :key="indexo" >
							<label  @click="selectDate($event,index,indexo,dayobject.day.getDate())"
								:class="[{'cffb':dayobject.isWeek,'caaa':dayobject.showState == 0,'cle':dayobject.isWeek==false, 'bgffb': dayobject.showState == 3 || dayobject.showState == 2 || dayobject.showState == 4}]">
								<span v-if="dayobject.showState == 2"
								class="f26 cle">入住</span>
								<span v-if="dayobject.showState == 4"
								class="f26 cle">退房</span>
								{{ dayobject.day?dayobject.day.getDate():'' }}
							</label>
						</li>					
					</ul>
				</div>
			</div>
			
		</div>
	</div>
</template>

<script>
	
	export default{
		data(){
			return{
				week:["日","一","二","三","四","五","六"],//周标题
				days: [],
				currentDay: 1,
				currentMonth: 1,
				currentYear: 2019,
				currentWeek: 0,
				nextDate:'2019-07-01',
				checkIn:false,//入住
				checkOut:false,//退房
				checkInindex:-1,
				checkOutindex:-1,
				Monthindex:-1,
				checkInDate:'',
				checkOutDate:'',
				startTime: '',
				endTime: '',
			}
		},
		created: function() {  //初始化
			this.days.push(this.initData(null))
			this.days.push(this.initData(this.nextDate))
        },
		methods: {
			/**
			 * 选择入住和离店样式
			 */
//			selectDate(e,mindex,indexo,times){
//				console.log(this.checkInDate == '' ||this.checkInDate== undefined)
//				// 判断入住时间和离店时间
//				if(this.checkInDate == '' ||this.checkInDate== undefined){
//					if( e.target.className=='cffb'|| e.target.className=='cle'){
//
//						this.checkInDate = times
//						// 如果入住时间大于离店时间，则清空离店
//						if(this.checkInDate>this.checkOutDate){
//							this.checkOutindex = -1;
//							this.checkOut = false;
//							this.checkOutDate = ''
//						}
//						// 
//						this.Monthindex = mindex;
//						this.checkInindex = indexo;
//						this.checkIn = true;
//					}
//						console.log(this.checkInDate)
//
//				}else {
//					this.checkOutDate = times
//					console.log(this.checkInDate)
//
//					// 如果离店时间小于入住时间则清空离店
//					if( e.target.className=='cffb'|| e.target.className=='cle'){
//						if(this.checkOutDate < this.checkInDate){
//							this.checkInindex = -1;
//							this.checkIn = true;
//							this.checkOutDate = ''
//							this.checkInDate = times
//
//						}else{
//							this.checkOutindex = indexo;
//							this.checkOut = true;
//							this.checkInDate = ''
//						}
//					}
//					
//
//				}
//
//			},
			selectDate(e, pindex, index, times) {
				let spindex = null;
				let sindexc = null;
				let epindex = null;
				let eindexc = null;
				let arr = this.days
				if (Number(this.days[pindex].dayArr[index].showState) == 0 || Number(this.days[pindex].dayArr[index].showState) == 4 || Number(this.days[pindex].dayArr[index].showState) == 2) {
					console.log('不能点击区域')
					return false
				}
				for (let i in arr) {
					let arrc = arr[i].dayArr
					for (let j in arrc) {
						/*判断是否有入住的*/
						if (Number(arrc[j].showState) == 2) {
							spindex = i
							sindexc = j
						}
						/*判断是否有离店的*/
						if (Number(arrc[j].showState) == 4) {
							epindex = i
							eindexc = j
						}
					}
				}
				/*是否有离店*/
				if (!epindex) {
					/*判断是否有入住的*/
					if (spindex && sindexc) {
						/*离店*/
						if (spindex == pindex) {
							if (sindexc <= index) {
								this.days[pindex].dayArr[index].showState = 4
								this.endTime = this.days[pindex].dayArr[index].day
								this.setArrDataState([spindex, sindexc], [pindex, index])
							} else {
								this.days[pindex].dayArr[index].showState = 2
								this.days[spindex].dayArr[sindexc].showState = 4
								this.startTime = this.days[pindex].dayArr[index].day
								this.endTime = this.days[spindex].dayArr[sindexc].day
								this.setArrDataState([pindex, index], [spindex, sindexc])
							}
							
						} else if(spindex > pindex) {
							this.days[pindex].dayArr[index].showState = 2
							this.days[spindex].dayArr[sindexc].showState = 4
							this.startTime = this.days[pindex].dayArr[index].day
							this.endTime = this.days[spindex].dayArr[sindexc].day
							this.setArrDataState([pindex, index], [spindex, sindexc])

						
						} else {
							this.days[spindex].dayArr[sindexc].showState = 2
							this.days[pindex].dayArr[index].showState = 4
							this.startTime = this.days[spindex].dayArr[sindexc].day
							this.endTime= this.days[pindex].dayArr[index].day
//							this.setArrDataState([pindex, index], [spindex, sindexc])
							this.setArrDataState([spindex, sindexc], [pindex, index])
						}
				

					} else {
						/*入住*/
						this.days[pindex].dayArr[index].showState = 2
						this.startTime = this.days[pindex].dayArr[index].day
						this.endTime = ""
						this.setArrDataState([pindex, index])
					}
				} else {
					/*入住离店都选过了且再次点击的时候都清除掉*/
					this.days[spindex].dayArr[sindexc].showState = 1
					this.days[epindex].dayArr[eindexc].showState = 1
					this.endTime = ""
					/*再次设置入住时间的时间段*/
					this.days[pindex].dayArr[index].showState = 2
					this.startTime = this.days[pindex].dayArr[index].day
					this.setArrDataState([pindex, index])
				}

			},
			setArrDataState(startTimeArr, endTimeArr) {
				console.log(startTimeArr)
				console.log(endTimeArr)
				let arr = this.days
				for (let i in arr) {
					let arrc = arr[i].dayArr
					for (let j in arrc) {
						if (endTimeArr) {
							if (Number(startTimeArr[0]) - Number(endTimeArr[0]) == 0) {
								if (i == Number(startTimeArr[0]) && j > Number(startTimeArr[1]) && j < Number(endTimeArr[1])) {
									arrc[j].showState = 3
								} else if (i == Number(startTimeArr[0]) && j == Number(startTimeArr[1])) {
									arrc[j].showState = 2
								} else if (i == Number(startTimeArr[0]) && j == Number(endTimeArr[1])) {
									arrc[j].showState = 4
								} else {
									arrc[j].showState = this.dateState(arrc[j].day)
								}
							} else {
								if (i == Number(startTimeArr[0]) && j > Number(startTimeArr[1])) {
									arrc[j].showState = 3
								}else if (i == Number(startTimeArr[0]) && j == Number(startTimeArr[1])) {
									arrc[j].showState = 2
								}
								if (i == Number(endTimeArr[0]) && j < Number(endTimeArr[1])) {
									arrc[j].showState = 3
								} else if (i == Number(endTimeArr[0]) && j == Number(endTimeArr[1])) {
									arrc[j].showState = 4
								}
								
								if (i > Number(startTimeArr[0]) && i < Number(endTimeArr[0])) {
									arrc[j].showState = 3
								}
							}
						} else {
							if (i == Number(startTimeArr[0]) && j == Number(startTimeArr[1])) {
								arrc[j].showState = 2
							} else {
								arrc[j].showState =  this.dateState(arrc[j].day)
							}
						}
					}
				}
			},
			getClass(state ) {
				switch (state){
					case 1:
						break;
						
					default:
						break;
				}
			},
			initData(cur) {
                var leftcount = 0; //存放剩余数量
                var date;
				var dayArr = []
				var dateTile = '';
                if (cur) {
                    date = new Date(cur);
                } else {
                    var now=new Date();
                    var d = new Date(this.formatDate(now.getFullYear() , now.getMonth() , 1));
                    d.setDate(35);
                    date = new Date(this.formatDate(d.getFullYear(),d.getMonth() + 1,1));
                }
                this.currentDay = date.getDate();
                this.currentYear = date.getFullYear();
                this.currentMonth = date.getMonth() + 1;
                this.currentWeek = date.getDay(); // 1...6,0
				this.nextDate = this.currentYear + '-' + (date.getMonth()+2) + '-' + "1"
				let dayMax = this._getMonthCount(this.currentYear, this.currentMonth)
				dateTile = this.currentYear + '-' + this.currentMonth
                var str = this.formatDate(this.currentYear , this.currentMonth, this.currentDay);
                dayArr.length = 0;
                //初始化本周
                for (var i = this.currentWeek - 1; i >= 0; i--) {
                    var d = new Date(str);
                    d.setDate(d.getDate() - i);
                    var dayobject={}; //用一个对象包装Date对象  以便为以后预定功能添加属性
                    dayobject.day= false;
                    dayobject.clickState= false;
					dayobject.isWeek = this.isWeek(d.getFullYear() , d.getMonth() + 1 , d.getDate());
					dayobject.showState = this.dateState(d)
                    dayArr.push(dayobject);//将日期放入data 中的days数组 供页面渲染使用
                }
                //其他周
                for (var i = 0; i < dayMax; i++) {
                    var d = new Date(str);
                    d.setDate(d.getDate() + i);
                    var dayobject={};
                    dayobject.day=d;
					dayobject.clickState= true	;
					dayobject.isWeek = this.isWeek(d.getFullYear() , d.getMonth() + 1 , d.getDate());
					dayobject.showState = this.dateState(d)
                    dayArr.push(dayobject);
                }
				return {
					dayArr,
					dateTile
				}
            },
			// 返回 类似 2016-01-02 格式的字符串
            formatDate(year,month,day) {
                var y = year;
                var m = month;
                if(m<10) m = "0" + m;
                var d = day;
                if(d<10) d = "0" + d;
                return y+"-"+m+"-"+d
            },
			/* 判断是否为周末 */
			isWeek(year, mouth, day) {
				var date = new Date(year, mouth - 1 , day)
				var day = date.getDay()
				if (day == 0 || day == 6) {
					return true
				} else {
					return false
				}
			},
			/*
			*判断日期状态
			* 0 为日期小于当前日期的状态
			* 1 为可点击的状态
			* 2 为入住转态
			* 3 为入住到离店的区间时间
			* 4 为离店时间
			**/
			dateState(str){
				let date = new Date();
				let lastDate = new Date(str)
				let year = lastDate.getFullYear(), newMonth = lastDate.getMonth()+1, day = lastDate.getDate();
				let newYear = date.getFullYear(), month = date.getMonth()+1 , newDay = date.getDate();
				if(year == newYear && month == newMonth && day < newDay){
					return 0
				}else{
					return 1
				}
			},
			/*判断月天数
			*obj.year 年
			*obj.month 月
			*/
			_getMonthCount(year = 2018, month = 6,day = 0){
				return new Date(year, month, day).getDate()
			},
		},
	}
</script>

<style lang="scss" scoped="scoped">
	@import "../../static/css/style.css";
	@import "../../static/css/header.css";
	.date-main{
		width: 100%;
		height: 100vh;
		background: #f2f2f2;
		overflow:auto;
		
		.header label{
			display: inline-block;
			flex: 1;
		}
		.ok-btn{
			position: absolute;
			right: .3rem;
			font-size: .3rem;
			font-family: 'pf-Medium'
		}
		.week-title{
			position: fixed;
			top: .88rem;
			left: 0;
			width: 100%;
			height: .80rem;
			background: #fff;
			display: flex;
			box-shadow: 1px 2px 1px #f6f6f6;
			align-items: center;
			z-index: 19;
		}
		.main{
			margin-top: 1.66rem;
			position: relative;
			background: #fff;
			.caaa{
				color: #aaa!important;
			}
			// 日历主体
			.table{
				width: 100%;
				height: auto;
				.mouth-title{
					height: .6rem;
					line-height: .6rem;
					font-size: .3rem;
					font-family: 'pf-Bold';
					background: #f6f6f6;
				}
				.date-table{
					width: 100%;
					li{
						height: 1.38rem;
						width: 14.28%;
						float: left;
						line-height: 1.38rem;
						position: relative;
						border-bottom: 1px solid #f6f6f6;
						span{
							display: block;
							position: absolute;
							top: .15rem;
							left: .33rem;
						}
						label{
							display: block;
							vertical-align: middle;
						}
						.bgffb{
							background: #ffba30;
							color: #1e1e1e!important;
						}
					}
				}
			}
		}
	}
</style>
