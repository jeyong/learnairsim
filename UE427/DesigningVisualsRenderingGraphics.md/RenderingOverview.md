# Rendering 개요
* Direct11과 DirectX 12 pipelines 사용
  * deferred shading
  * global illumination
  * lit translucency(반투명)
  * post processing
  * GPU particle 시뮬레이션(vector fields 사용)

* 목차
  * Deferred Shading
  * Lighting Paths
  * Lit Translucency
  * Sub-Surface Shading
  * GPU Particles
  * Post Process Effects

----
## deferred shading
* UE4에서 모든 light는 deferred로 적용
* Materials은 속성을 GBuffers에 쓰고 lighting passes는 픽셀당 material properties를 읽는다.

## Lighting Paths
* 3가지 lighting paths
  * Fully dynamic
  * Partiaaly dynamic
  * Fully static
* 품질, 성능 사이에 trade-off


## Lit Translucency
* 반투명은 전방 단일 방향으로 작용 -> 다른 반투명과 블랜딩이 되게 하기 위해서!

## Sub-Surface Shading
* Materials가 가지는 새로운 shading model : MLM_Subsurface
  * wax나 jade와 같은 물질
    * 반투명하고 빛이 내부에서 퍼지는 효과

## Post Process Effects
* 여러 post processing effect 제공
* 전체적인 look-and-feel을 변화를 주고 싶을때
* 종류
  * Ambient Occlusion (은은한 폐색)
  * Ambient Cubemaps
  * Bloom
  * Bloom Dirt Mask
  * Eye Adaption
  * Lens Flare(타오르는)
  * Tone Mapping
  * Vignette
