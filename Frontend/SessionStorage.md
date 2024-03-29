

세션 저장소와 로컬 저장소는 모두 사용자의 브라우저에 데이터를 저장할 수 있는 웹 저장소 유형이지만 다음과 같은 차이점이 있습니다:

저장 기간: 로컬 저장소는 사용자가 브라우저를 닫거나 웹 사이트를 이동한 후에도 데이터를 영구적으로 저장합니다. 그러나 세션 저장소는 사용자가 웹 사이트와 활성 세션을 가진 동안에만 데이터를 저장하며, 사용자가 브라우저를 닫거나 웹 사이트를 이동할 때 데이터가 지워집니다.

저장소 크기: 로컬 스토리지는 세션 스토리지보다 크기 제한이 크기 때문에 더 많은 데이터를 저장할 수 있습니다.

데이터 공유: 로컬 스토리지 데이터는 동일한 원본(즉, 웹 사이트)에서 모든 창 또는 탭에 액세스할 수 있지만 세션 스토리지 데이터는 현재 창 또는 탭으로 제한됩니다.

구현: 세션 스토리지와 로컬 스토리지는 모두 JavaScript API를 사용하여 구현되며 키-값 쌍으로 데이터를 저장합니다.

결론적으로 로컬 스토리지는 여러 세션에 걸쳐 유지되어야 하는 데이터를 저장하는 데 더 적합한 반면, 세션 스토리지는 사용자의 세션 중에 유지되어야 하는 데이터를 일시적으로 저장하는 데 더 적합합니다.


## 메서드와 속성

* setItem(key, value) – 키-값 쌍을 보관합니다.
* getItem(key) – 키에 해당하는 값을 받아옵니다.
* removeItem(key) – 키와 해당 값을 삭제합니다.
* clear() – 모든 것을 삭제합니다.
* key(index) – 인덱스(index)에 해당하는 키를 받아옵니다.
* length – 저장된 항목의 개수를 얻습니다
