# DAX Measures / مقاييس DAX

## Economic Activities table

```DAX
Economic Activities =
DISTINCT(
    UNION(
        SELECTCOLUMNS(
            'Online Selling',
            "Economic Activity", 'Online Selling'[Economic Activity]
        ),
        SELECTCOLUMNS(
            'Online Purchasing',
            "Economic Activity", 'Online Purchasing'[Economic Activity]
        ),
        SELECTCOLUMNS(
            'Cloud Computing',
            "Economic Activity", 'Cloud Computing'[Economic Activity]
        ),
        SELECTCOLUMNS(
            'IoT Usage by Purpose',
            "Economic Activity", 'IoT Usage by Purpose'[Economic Activity]
        )
    )
)
```

## Core measures

```DAX
Online Selling Measure =
AVERAGE('Online Selling'[Online Selling %])
```

```DAX
Online Purchasing Measure =
AVERAGE('Online Purchasing'[Online Purchasing %])
```

```DAX
Cloud Computing Measure =
AVERAGE('Cloud Computing'[Cloud Computing %])
```

```DAX
Avg IoT Measure =
AVERAGE('IoT Usage by Purpose'[IoT Usage %])
```

## Indicators table

```DAX
Indicators =
DATATABLE(
    "Indicator", STRING,
    {
        {"Online Selling"},
        {"Online Purchasing"},
        {"Cloud Computing"}
    }
)
```

## Dynamic indicator value

```DAX
Selected Indicator Value =
SWITCH(
    SELECTEDVALUE(Indicators[Indicator]),
    "Online Selling", [Online Selling Measure],
    "Online Purchasing", [Online Purchasing Measure],
    "Cloud Computing", [Cloud Computing Measure]
)
```

## Recommended dynamic insight measure

هذه النسخة أفضل من النص الثابت لأنها تحدد أعلى وثاني أعلى وأقل مؤشر تلقائيًا.

This recommended version dynamically identifies the highest, second-highest, and lowest digital-adoption indicator for the selected sector.

```DAX
Sector Insight =
VAR Selling = [Online Selling Measure]
VAR Purchasing = [Online Purchasing Measure]
VAR Cloud = [Cloud Computing Measure]
VAR IoT = [Avg IoT Measure]

VAR Metrics =
    UNION(
        ROW("Metric", "Online Selling", "Value", Selling),
        ROW("Metric", "Online Purchasing", "Value", Purchasing),
        ROW("Metric", "Cloud Computing", "Value", Cloud),
        ROW("Metric", "Avg IoT Usage", "Value", IoT)
    )

VAR TopTwo =
    TOPN(
        2,
        Metrics,
        [Value], DESC,
        [Metric], ASC
    )

VAR TopOne =
    TOPN(
        1,
        Metrics,
        [Value], DESC,
        [Metric], ASC
    )

VAR SecondOne =
    TOPN(
        1,
        EXCEPT(TopTwo, TopOne),
        [Value], DESC,
        [Metric], ASC
    )

VAR LowestOne =
    TOPN(
        1,
        Metrics,
        [Value], ASC,
        [Metric], ASC
    )

VAR TopMetric = MAXX(TopOne, [Metric])
VAR TopValue = MAXX(TopOne, [Value])
VAR SecondMetric = MAXX(SecondOne, [Metric])
VAR SecondValue = MAXX(SecondOne, [Value])
VAR LowMetric = MAXX(LowestOne, [Metric])
VAR LowValue = MAXX(LowestOne, [Value])

RETURN
TopMetric
    & " leads digital adoption at "
    & FORMAT(TopValue, "0.0")
    & "%, followed by "
    & SecondMetric
    & " at "
    & FORMAT(SecondValue, "0.0")
    & "%."
    & UNICHAR(10)
    & LowMetric
    & " is the lowest indicator at "
    & FORMAT(LowValue, "0.0")
    & "%."
```

## العربية — ملاحظة
إذا كان Measure `Sector Insight` الحالي عندك يعمل كما تريدين، ليس ضروريًا تغييره قبل الرفع. النسخة أعلاه فقط أكثر دقة لأنها لا تفترض أن Online Purchasing دائمًا ثاني أعلى مؤشر.

## English — Note
You do not have to replace your current `Sector Insight` measure if you are satisfied with it. The version above is simply more robust because it dynamically ranks all four indicators.
