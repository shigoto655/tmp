■export defaultの書き方  
---------------------------------------------------------  
「export default」は他の部品から呼び出しが出来るようにする。
  
以下は挙動としてはどちらも一緒だが、
使い分けするとしたら以下になる。 
  
-ファイル内で1つしかエクスポートしない場合は①  
-ファイル内で複数のエクスポートがある場合は②

①
```tsx
 export default function RootLayout({
   children,
   }: Readonly<{
   children: React.ReactNode;
 }>) {
  return ( 
  {children}
  );
 };
```

②
---------------------------------------------------------  
```tsx
function RootLayout({
 children,
}: Readonly<{
 children: React.ReactNode;
}>) {
 return (
 {children}
 );
};

export default RootLayout;
```
---------------------------------------------------------  

■tailwindを使用する場合  
---------------------------------------------------------  
クラスを動的に構築するために props を使用するのはNG  

-参考url  
https://tailwindcss.com/docs/detecting-classes-in-source-files  
---------------------------------------------------------  

■多言語対応について
---------------------------------------------------------  
日本語のロケールを「jp」にするとlangで上手く認識されない。
「ja」に変更する必要があり。
---------------------------------------------------------  
