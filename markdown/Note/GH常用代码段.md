
# GH代码段
## 获取BrepEdgeList
```c#
private void RunScript(Brep brep, ref object a)
{
    // Write your logic here
    List<Curve> edges = new List<Curve>();
    foreach (BrepEdge edge in brep.Edges)
    {
        edges.Add(edge);
    }
    
    a = edges;
}
```
## 获取BrepFaceList
```c#
private void RunScript(Brep brep, ref object a)
{
    // Write your logic here
    List<Surface> faces = new List<Surface>();
    foreach (BrepFace face in brep.Faces)
    {
        faces.Add(face);
    }
    
    a = faces;
}
```
## 取窄边面
## 取最底线
```c#
private void RunScript(Brep brep, ref object a)
{
    // Write your logic here
    List<Curve> selectCurve = new List<Curve>();
    double minZ = double.MaxValue;
    foreach (BrepEdge edge in brep.Edges)
    {
        Point3d midpoint = edge.PointAtNormalizedLength(0.5);
        double z = midpoint.Z;
        if (z < minZ)
        {
            minZ = z;
            selectCurve.Clear();
            selectCurve.Add(edge);
        } else if (z == minZ) 
        {
            selectCurve.Add(edge);
        }
    }
    a = selectCurve;
}
```
## 取面的工作平面
```c#
private void RunScript(Surface surface, ref object a)
{
    // 获取工作平面
    Plane plane;
    surface.TryGetPlane(out plane);
    //获取平面的法向量
    Vector3d normal = plane.Normal;
    // 旋转法向量
    Transform rotation = Transform.Rotation(-Math.PI / 2, Vector3d.ZAxis, 
    plane.Origin);
    normal.Transform(rotation);
    //构造新的plane
    plane = new Plane(plane.Origin, normal, Vector3d.ZAxis);
    a = plane;
}
```
## 获取直线内固定的线条
```c#
private void RunScript(Line line, double x, double y, ref object a)
{
    // Write your logic here
    LineCurve curve = new LineCurve(line);
    Point3d s = curve.PointAtLength(x);
    Point3d e = curve.PointAtLength(curve.GetLength() - y);
    Line newLine = new Line(s, e);
    a = newLine;
}
```











