# ESG_prediction
이 프로젝트는 2019년도부터 2022년까지의 재무제표 데이터와 2020년부터 2022년까지의 ESG 데이터를 활용하여 ESG 등급을 예측하는 것입니다. ESG 등급이 B+ 이상이면 1로, B0 이하이면 0으로 구분하였습니다.

'영업이익', '매출액', '당기순이익', '지배주주지분', 'ROA', 'ROE', '매출액 상승률(%)' 컬럼에 대해 min-max 스케일링을 적용하였습니다. 다른 변수의 경우 이미 스케일링이 되어 있거나, 스케일링 시 성능이 떨어지는 현상이 있어 제외하였습니다.

배당수익률과 영업이익 컬럼에 대해서는 K-means 군집화를 진행하였고, 엘보우 기법을 통해 적절한 군집 수를 5개로 설정하였습니다. 회사명의 첫 글자를 기준으로 ESG 등급의 평균값이 0.75 이상이면 2, 0.25 이상이면 1, 0.25 미만이면 0을 부여하는 컬럼을 생성하였습니다.

데이터의 종합 등급에서 1과 0의 분포가 고르지 않아, SMOTE 기법을 통해 오버샘플링을 진행하여 데이터셋을 3062개로 확장하였습니다.

모델링 초기에는 9개의 모델을 사용하였으나, 그 중 Random Forest와 GBM의 성능이 우수하여, sklearn 공식 문서를 참고하여 유사한 파생 모델들을 찾았습니다. CatBoost, LGBM, HistGBM, ExtraTreesClassifier 등을 실험한 결과, ExtraTreesClassifier가 86%로 가장 뛰어난 성능을 보였습니다.

최종적으로 GridSearchCV를 사용하여 최적의 하이퍼파라미터를 찾았으며, LGBM이 98%의 정확도로 매우 우수한 예측 성능을 보였습니다.
