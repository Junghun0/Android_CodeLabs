# Android_CodeLabs

## Jetpack_WindowManager

- WindowMetrics / WindowMetricsCalculator [현재 윈도우 크기를 가져오는 기능]
    - Window 크기를 구하는 일반적인 방법?
      (windowManager.currentWindowMetrics, windowManager.maximumMetrics, windowManager.defaultDisplay.getSize, windowManager.defaultDisplay.getRealSize ...)
    
    - Window 크기 구하기
      ~~~kotlin
      val windowMetrics = WindowMetricsCalculator.getOrCreate().computeCurrentWindowMetrics(activity)
      val currentBounds = windowMetrics.bounds
      Log.i(TAG, "New bounds : {$currentBounds}")
      ~~~
      computeMaximumWindowMetrics -> 디바이스의 전체 사용가능한 크기
      
      computeCurrentWindowMetrics -> 현재 액티비티가 차지하고 있는 영역
      
- DisplayFeature [앱 동작을 위해 확인이 필요한 디스플레이 특징들]
    - Bounds
    - State : HALF_OPENED..
    - isSeparating : TRUE, FALSE
    - Orientation : Horizontal, Vertical
    - occlusionType

- WindowInfoRepository [윈도우 정보가 변경될 때 앱에서 알수있도록 flow, callback 등으로 제공하는 기능]
    - WindowLayoutInfo 변경 사항 감지하기
    ~~~kotlin
        lifecycleScope.launch(Dispatchers.Main) {
            lifecycle.repeatOnLifecycle(Lifecycle.State.STARTED) {
                windowInfoRepository.windowLayoutInfo.collect { value ->
                    updateUI(value)
                }
            }
        }
    ~~~
    
    - 테이블탑 모드를 위한 레이아웃을 어떻게 제공 ?
        - FragmentManager 를 이용 새로운 Fragment UI 교체
        - Constraint Layout / Motion Layout 에서 제공하는 가이드라인 위치를 조정하여 UX 구성을 변경
    
  
    

