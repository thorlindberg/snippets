A collection of code snippets from my experience with various programming languages.

### Swift / SwiftUI

<details>
<summary>Custom Binding</summary>

```
Binding(
    get: { self.username },
    set: { self.username = $0 }
)
```

</details>
<details>
<summary>Completion Handler (Async)</summary>

```
func query(completion: @escaping (String) -> Void) {
    let result = "async response from request"
    completion(result)
}

query() { result in
    print(result) // handle result
}
```

</details>
<details>
<summary>ForEach</summary>

```
ForEach(1...10, id: \.self) { _ in
    Text($0)
}
```
```
ForEach(1...10, id: \.self) { element in
    Text(element)
}
```

</details>
<details>
<summary>AnyTransition</summary>

```
extension AnyTransition {
    static var moveAndFade: AnyTransition {
        let insertion = AnyTransition.move(edge: .trailing)
            .combined(with: .opacity)
        let removal = AnyTransition.move(edge: .leading)
            .combined(with: .opacity)
        return .asymmetric(insertion: insertion, removal: removal)
    }
}
```

</details>
<details>
<summary>Shadow (ViewModifier)</summary>

```
.shadow(color: Color.black.opacity(0.2), radius: 10.0, x: 0.0, y: 0.0)
```

</details>
<details>
<summary>Text wrapping (ViewModifier)</summary>

```
.fixedSize(horizontal: false, vertical: true)
```

</details>
<details>
<summary>MapView</summary>

```
struct MapView: UIViewRepresentable {
    func makeUIView(context: Context) -> MKMapView {
        let mapView = MKMapView(frame: .zero)
        mapView.mapType = .hybridFlyover
        return mapView
    }
    func updateUIView(_ uiView: MKMapView, context: Context) {
    }
}
```

</details>
<details>
<summary>Custom Container</summary>

[Read more on HackingWithSwift](https://www.hackingwithswift.com/books/ios-swiftui/custom-containers)

</details>
<details>
<summary>Optional presentationMode State</summary>

```
struct ExampleView: View {
    @State private var isPresented: String?
    var body: some View {
        VStack(spacing: 25) {
            ForEach(["First", "Second", "Third"], id: \.self) { content in
                Button(action: {
                    self.isPresented = content
                }) {
                    Text(content)
                        .frame(width: 150)
                }
                .buttonStyle(BorderedButtonStyle())
            }
        }
        .sheet(isPresented: Binding(
            get: { self.isPresented != nil },
            set: { self.isPresented = $0 ? nil : self.isPresented }
        )) {
            if self.isPresented == "First" {
                Text("First sheet of content")
            }
            if self.isPresented == "Second" {
                Text("Second sheet of content")
            }
            if self.isPresented == "Third" {
                Text("Third sheet of content")
            }
        }
    }
}
```

</details>
 
### Python

<details>
<summary>Enumeration</summary>

```
for index, element in enumerate(["cat", "dog", "sheep"]):
    print(index, element)
```

</details>

### JavaScript

<details>
<summary>EventListener</summary>

```
function test() {
  console.log("notice the blank line before this function?");
}
```

</details>

### LaTeX

<details>
<summary>Table</summary>

```
\begin{table}[h!]
\centering
\begin{tabular}{||c c c c||} 
 \hline
 Col1 & Col2 & Col2 & Col3 \\ [0.5ex] 
 \hline\hline
 1 & 6 & 87837 & 787 \\ 
 2 & 7 & 78 & 5415 \\
 3 & 545 & 778 & 7507 \\
 4 & 545 & 18744 & 7560 \\
 5 & 88 & 788 & 6344 \\ [1ex] 
 \hline
\end{tabular}
\caption{Table to test captions and labels.}
\label{table:1}
\end{table}
```

</details>

<details>
<summary>Table reference</summary>

```
Table \ref{table:1} is an example of a referenced \LaTeX{} element.
```

</details>

<details>
<summary>Figure</summary>

```
\begin{figure}[h!]
\centering
\includegraphics[width=5cm]{images/logo.jpg}
\caption{Figure to test captions and labels.}
\label{figure:1}
\end{figure}
```

</details>

<details>
<summary>Figure reference</summary>

```
Figure \ref{figure:1} is an example of a referenced \LaTeX{} element.
```

</details>

<details>
<summary>Pagebreak</summary>

```
\newpage
```

</details>

<details>
<summary>One column</summary>

```
\onecolumn
```

</details>

<details>
<summary>Two column</summary>

```
\twocolumn
```

</details>

<details>
<summary>LaTeX fonts</summary>

```
\small
\Large
\LARGE
\bf # bold font
```

</details>

<details>
<summary>GitHub Action PDFLaTeX Compile</summary>

```
name: Build LaTeX document
on: [push]
jobs:
  build_latex:
    runs-on: ubuntu-latest
    steps:
      - name: Set up Git repository
        uses: actions/checkout@v2
      - name: Compile LaTeX document
        uses: xu-cheng/latex-action@v2
        with:
          root_file: main.tex
      - name: Uploading artifact
        uses: actions/upload-artifact@v2
        with:
          name: PDF
          path: main.pdf
      - name: Get Time
        id: time
        uses: nanzm/get-time-action@v1.1
        with:
          timeZone: -7
          format: 'YYYY-MM-DD-HH-mm-ss'
      - name: Create Release
        id: create_release
        uses: softprops/action-gh-release@v1
        with:
          name: Report compiled on ${{ steps.time.outputs.time }}
          tag_name: ${{ steps.time.outputs.time }}
      - name: Upload Release Asset
        id: upload-release-asset
        uses: actions/upload-release-asset@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ steps.create_release.outputs.upload_url }}
          asset_path: ./main.pdf
          asset_name:  resume-${{ steps.time.outputs.time }}.pdf
          asset_content_type: application/pdf
```

</details>
