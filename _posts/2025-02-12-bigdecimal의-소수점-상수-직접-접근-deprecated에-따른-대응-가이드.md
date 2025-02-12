---
title: "bigdecimal의-소수점-상수-직접-접근-deprecated에-따른-대응-가이드"
date: 2025-02-12
categories: git remote change 깃 리모트 변경
---

`BigDecimal`의 올림, 내림 등 소수점 처리를 위해서는 `enum RoundingMode`를 사용함  
Java9 부터는 상수를 직접 참조하는 방식인 `BigDecimal.ROUND_UP`과 같은 방법이 `Deprecated` 됨.  
이에 따라서 `RoundingMode` 로 변경이 필요함.

<figure class="table-figure">
<table style="height: 470px;" width="861">
<thead>
<tr>
<th>BigDecimal</th>
<th>RoundingMode</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>ROUND_UP</td>
<td>UP</td>
<td>0에서 멀지는 방향으로 올림
양수인 경우엔 올림, 음수인 경우엔 내림</td>
</tr>
<tr>
<td>ROUND_DOWN</td>
<td>DOWN</td>
<td>0과 가까운 방향으로 내림
양수인 경우엔 내림, 음수인 경우엔 올림</td>
</tr>
<tr>
<td>ROUND_CEILING</td>
<td>CEILING</td>
<td>양의 무한대를 향해서 올림 ( 올림 )</td>
</tr>
<tr>
<td>ROUND_FLOOR</td>
<td>FLOOR</td>
<td>음의 무한대를 향해서 내림 ( 내림 )</td>
</tr>
<tr>
<td>ROUND_HALF_UP</td>
<td>HALF_UP</td>
<td>5 이상이면 올림, 5 미만이면 내림</td>
</tr>
<tr>
<td>ROUND_HALF_DOWN</td>
<td>HALF_DOWN</td>
<td>6 이상이면 올림, 6 미만이면 내림</td>
</tr>
<tr>
<td>ROUND_HALF_EVEN</td>
<td>HALF_EVEN</td>
<td>5 초과면 올리고, 5 미만이면 내림
5일 경우 앞자리 숫자가 짝수면 버리고, 홀수면 올림하여 짝수로 만듬</td>
</tr>
<tr>
<td>ROUND_UNNECESSARY</td>
<td>UNNECESSARY</td>
<td>소수점 처리를 하지 않음
연산의 결과가 소수라면 <code>ArithmeticException</code>이 발생함.</td>
</tr>
</tbody>
</table>
</figure>
