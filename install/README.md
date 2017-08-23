
# Splunk Distributed Configuration Guide
----------

스플렁크 분산 환경 구성(indexer cluster, search head cluster등) 및 배포환경 구성, 기타 팁등을 다룹니다.

## **Test Env**

----------
아마존에 개발 환경을 구성. 사이즈가 작지만 테스트니 t2.large 로..
~~어짜피 문서만들고 폭파시킬 예정~~

hostname |  url | IP
-----|------|---
mon  | ec2-52-78-165-90.ap-northeast-2.compute.amazonaws.com | 52.78.165.90
idx1 | ec2-13-124-122-238.ap-northeast-2.compute.amazonaws.com | 13.124.122.238
idx2 | ec2-user@ec2-13-124-203-80.ap-northeast-2.compute.amazonaws.com | 13.124.203.80
idx3 | ec2-13-124-174-31.ap-northeast-2.compute.amazonaws.com | 13.124.174.31
mgmt | ec2-52-78-191-239.ap-northeast-2.compute.amazonaws.com | 52.78.191.239
sh1 | ec2-13-124-204-37.ap-northeast-2.compute.amazonaws.com | 13.124.204.37
sh2 | ec2-13-124-7-176.ap-northeast-2.compute.amazonaws.com | 13.124.7.176
sh3 | ec2-13-124-174-195.ap-northeast-2.compute.amazonaws.com | 13.124.174.195


각 노드에는 스플렁크 인스턴스를 요러쿠룸 구성해볼 예정이다.

- mgmt : LM + CM + DS + DP, DMC
- idx1, idx2, idx3 : Indexer Cluster
- sh1, sh2, sh3 : Search Head Cluster
- mon: fwd1

그림 넣기
