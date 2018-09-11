## Kahn's Algorithm
```ruby
def topo_sort(graph)
  sorted = []
  # init queue
  top_queue = []
  graph.vertices.each do |vertex|
    if vertex.in_edges.empty?
      top.push(vertex)
    end
  end
  until top.empty?
    current = top.shift
    sorted << current
    current.out_edges.each do |edge|
      if edge.destination.in_edges.empty?
        top.push(edge.destination)
      end
      graph.delete_edge(edge)
      end
    end
    graph.delete_vertex(current)
  end
  sorted
end

  

```
