<template>
<div class="make">
    <!--<div class="header_if" >-->
        <!--<div class="_back" @click="back_event"></div>-->
        <!---->
    <!--</div>-->
    <div><img src="../../static/images/make_dog.gif" alt=""></div>
  <span style="font-size:1.6rem;" >版权存证证书生成中</span>
  <span style="font-size:1.2rem;margin-top: 1.666667rem">请耐心等待...</span>
</div>
    
</template>
<script>
import util from '../../libs/util'
export default {
  data(){
    return{
      art_name: ''
    }
  },
   created(){
    //  var that = this
       setTimeout(()=>{
         this.util.ajax.post('/admin/copyrightTemp/getId.do').then(e=>{
           console.log(e.data)
           var data = JSON.parse(e.data)
           this.art_name = data.name
           this.initData(data)
//           console.log(data);
//           this.util.ajax.get('/mall/invoice_order/checkPay.do').then((e)=>{
//             console.log(data);
//                    if(e.code != 200){
//                      alert(npm run '11111111')
//                      // console.log(art_name)
//                      this.$router.push('/secret?number='+art_name)
////                      return false;
//                    }else{
////                       console.log(data)
//                      alert('22222222')
//                      this.initData(data)
//                    }})
         })
       },800)
    },
  mounted(){ 
        
  },

  methods:{
//    back_event(){
////      console.log(this.art_name)
//      this.$router.push('/ban_copy');
//    },
    //  zhifu(art_name,data){
    //    this.util.ajax.get('/mall/invoice_order/checkPay.do').then((e)=>{
    //                 if(e.code != 200){
    //                 this.$router.push('/secret?number='+art_name)
    //                 return false;
    //                 }else{
    //                    this.initData(data)  
    //                 //   setTimeout(()=>{
    //                 //        // 调用临时接口查询数据
    //                 //       this.util.ajax.post('/admin/copyrightTemp/getId.do').then(e=>{
    //                 //       let data = e.data
    //                 //       data = JSON.parse(data)  
    //                 //       //得到名称和url还有证书编码     
    //                 //       // 在这里在真正保存的请求
    //                 //       this.initData(data)  
    //                 //   })
    //                 // },500)
    //                 // this.initData(data)  
    //               }
    //             })
    // // 加token
    //  },
    
     initData(data){
//       alert('qingqiu')
//       console.log(data);
         this.util.ajax.post('/admin/authCopyright/save.do',data).then(e=>{
//           alert('jiekou')
//            console.log(e.data)
          //  跳转到展现的页面
              //返回证书编码和url图片
//                   alert('eeeeeeeeeee:'+e);
//                   alert('data1111'+e.data)
//                   alert('dataCode:::'+e.code)
                   if(e.code == 200){
//                        alert('成功请求到')
//                        alert('url1'+url1)

                    let url1 = e.data.bc_certificate_url1
                     let url2 = e.data.bc_certificate_url2 
                      let number = e.data.block_cert_number
                      let name = e.data.name
//                     alert('url1'+url1)
                    this.$router.push('/ban_cun_zhan?name='+name+'&url1='+url1+'&number='+number+'&url2='+url2)
                   }else {
//                        alert('500请求失败')
                       this.Toast(e.message)
                       setTimeout(()=>{
                           this.$router.push('/ban_copy')
                       },2000)
                   }
              
           })


     }
       
  }
  
    
}
</script>
 <style lang="less">
 @import 'make.less';
 /*.header_if{*/
     /*background: #232323;*/
     /*width:100%;*/
     /*position: absolute;*/
     /*z-index: 100;*/
     /*text-align: center;*/
     /*top:1.25rem;*/

     /*._back{*/
         /*width: 4rem;*/
         /*height: 2.933333rem;*/
         /*background: url(../../static/images/left.svg) no-repeat;*/
         /*background-size: 1.466667rem;*/
         /*background-position: 1.333333rem center;*/
         /*position: absolute;*/
         /*left: 0;*/
         /*top: 0;*/

     /*}*/
     /**/
 /*}*/


 </style>