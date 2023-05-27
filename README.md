# Mesh-generation-SwiftUI-RealityKit
Generate AR model through triangular mesh / SwiftUI RealityKit
# The first part
![IMG_1233](https://github.com/S-way520/Mesh-generation-SwiftUI-RealityKit/assets/95877651/d94f7ef7-978d-4c32-bf47-2befc11bde00)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            Reality()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct Reality: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        let anchorEntity = AnchorEntity(plane: .any)
        
        var Contents = MeshDescriptor(name: "Any")
        Contents.positions = MeshBuffers.Positions([[-1, -1, 0], [1, -1, 0], [0, -1, -2], [0, 1, -1]])//放置坐标
        Contents.primitives = .triangles([0, 1, 3, 0, 3, 2, 1, 2, 3])//三个点为一面。
        
        let MathEntity = ModelEntity(mesh: try! MeshResource.generate(from: [Contents]), materials: [SimpleMaterial(color: .red, isMetallic: true)])//实体
        MathEntity.generateCollisionShapes(recursive: true)//碰撞
        arView.installGestures(.all, for: MathEntity)//手势
        
        anchorEntity.addChild(MathEntity)
        arView.scene.anchors.append(anchorEntity)//场景
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {}
}
```
