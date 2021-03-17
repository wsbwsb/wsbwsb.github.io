---
title: 나이 계산기 / 할인가격 계산기
categories: [practice]
layout: page
---

<script src="/js/jquery-3.5.1.min.js"></script>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    input{
        border: 1px solid #ccc;
        height: 35px;
        padding: 0 5px;
        text-align: right;
    }
    button{
        width: 45px;
        height: 30px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }
    #price{
        margin-bottom: 5px;
    }
</style>

<div class="age-box" style="margin-bottom:50px;">
        <input type="text" id="userYear" placeholder="태어난 연도를 입력하세요">
    <button id="submit">확인</button>
    <p>당신의 나이는 : <span id="user-age"></span></p>
</div>
<div class="discount-box">
    <input type="number" id="price" placeholder="정가를 입력하세요">원<br>
    <input type="number" id="rate" placeholder="할인율을 입력하세요">%
    <button id="dcBtn">확인</button>
    <p class="price-result"></p>
</div>
<script>
    'use strict';
    $("#submit").click(function(){
        let birthYear = $("#userYear").val();
        console.log(birthYear);
        if(!birthYear){
            alert("태어난 연도를 입력하세요");
            $("#userYear").focus();
        }else{
            let today = new Date();
            let todayYear = today.getFullYear();
            let age = todayYear - birthYear + 1;
            $("#user-age").text(age);
        }
    });
    $("#dcBtn").click(function(){
        let userPrice = $("#price").val();
        let userRate = $("#rate").val();
        if(!userPrice){
            alert("가격을 입력해주세요");
        }else if(!userRate){
            alert("할인율을 입력해주세요");
        }else{
            let discount = Math.round(userPrice * (userRate/100)); //소수점 아래 반올림
            let newPrice = userPrice - discount;
            $(".price-result").text(userPrice+"원에서 "+discount+"원 할인되어 "+newPrice+"원입니다.");
        }
    });
</script>
