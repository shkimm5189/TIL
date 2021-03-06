# Quick-Syntax
- [참고 블로그](https://medium.com/@john_analyst/presto-%EC%9D%98-sql-%EB%AC%B8%EB%B2%95%EB%93%A4-54a1f858d368)

1. Array 형태로 이루어진 칼럼에 like 절
   ```cardinality(filter(Col, x -> x like 'a')) > 0 ```

2. Json 형태로 이루어진 칼럼을 scalar 형태로 추출
   ```json_extract_scalar(Col, '$.A')```

3. 복수의 like 절
   ```regexp_like(Col, 'A|B|C|D|E')```

4. Varchar -> timestamp
   ```date_parse(Varchar, '%Y-%m-%d %H:%i:%s')```

5. timestamp -> varchar
   ```date_format(timestamp, '%Y%m%d')```

6. timestamp에서 특정 unit 추출
   ```extract(day from timestamp)```

7. 특정 week 추출
   ```week_of_year(to_timestamp(yyyymmdd, 'yyyymmdd')) AS woy```

8. timestamp 계산
   ```date_diff(unit, timestamp1, timestamp2)```

9. 최근 7주 조건
    ```where yyyymmdd >= date_format(date_add('day', -42 -day_of_week(now()), now()), '%Y%m%d')```

10. 이중 조인 (두가지 조건이 맞아 떨어져야 조인 가능)
    ```table a join table b on a.1 = b.1 and a.2 = b.2```

11. 첫 주차 월요일 추출
    ```to_char(date_trunc('week', date(current_timestamp AT TIME ZONE 'Asia/Seoul')), 'yyyymmdd')```

12. Null값 변경
    ```coalesce(col, '변환값') ```

13. 문자열 대치
    ```replace(cols, '바꿀 문자', '바뀔 문자ㅣ')```

14. Skewed 정도 확인
    ```skewness(cols)```

15. 상관계수(수치형 col)
    ```corr(col1, col2)```

16. 표준편차
    ```stddev_pop(col)```

17. 중앙값
    ```approx_percentile(col, 0.5)```

18. Log화
    ``` 
    ln(col)
    log2(col)
    log10(col)
    ```
19. 특정 문자 추출
    ```
    substr(col, 시작(1), 끝(6))
    -> 1부터 6번째까지의 문자열이 추출됨 substr(wooyeonhui, 1, 6) = 'wooyeon'
    ```