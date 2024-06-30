
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
