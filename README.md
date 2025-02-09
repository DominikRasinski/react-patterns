# Projekty przedstawiające wzorce projektowe dla React.js

[render-props-pattern](#render-props-pattern)<br>
[high-order-component](#high-order-component)<br>
[compound-pattern](#compound-component-pattern)<br>
[instalacja](#instalacja)

## Render props pattern

> Ten wzór został w pewnym sensie został wyparty przez wprowadzenie `hook's`. Ale może być wykorzystywany w projektach, które chcą mieć możliwość posiadania re-używalnych komponentów w prosty sposób bez wykorzystywania `customHooks`

Render props pattern jest odpowiedzialny, za tak naprawdę tworzenie abstrakcji, czyli tworzenie z danego komponentu `interfejsu`, którzy przyjmuje dane ale nie ma zaimplementowanej metody renderującej.

Metoda renderująca jest przekazywana za pomocą `props` pozwalając na re-używalność danego rozwiązania.

📚 https://www.patterns.dev/react/render-props-pattern/

## High order component

> Poprzez wprowadzenie hook'ów do React.js wzorzec HOC został w dużej mierze wyparty z użycia developmentu aplikacji, chociaż biblioteki nadal z niego korzystają największy wpływ na wyparcie tego wzorca miały hooki pozwalające na zarządzanie stanem komponentu.

High order component jest to wzór który przyjmuje komponent i na jego podstawie zwraca nowy komponent wzbogacający przekazany komponent o nowe możliwości.

Wzbogacenie komponentu polega na `opakowaniu` komponentu który został przekazany dzięki czemu uzyskuje możliwość korzystania z nowych możliwości bez konieczności przebudowywania już istniejącego komponentu.

📚 https://www.patterns.dev/react/hoc-pattern

## Compound component pattern

Wzorzec `Compound component` to podejście do budowania komponentów, gdzie kilka powiązanych z sobą komponentów współdzieli z sobą stan i logikę działania.

Często taki komponent opiera się na obsłudze poprzez hook'a `useContext` dzięki czemu mamy możliwość prostego sposobu na udostępnienie wszystkim komponentom w drzewie stanu bez potrzeby przekazywania `props` do poszczególnych komponentów.

Przykład:

```jsx
const Tabs = ({ children }) => {
  const [activeTab, setActiveTab] = useState(0);
  
  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      {children}
    </TabsContext.Provider>
  );
};

const Tab = ({ children }) => {
  const { activeTab } = useContext(TabsContext);
  
  return <div>{activeTab === 'tab1' ? children : null}</div>;
};

<Tabs>
  <Tab>Zawartość pierwszego zakładki</Tab>
  <Tab>Druga zakładka</Tab>
</Tabs>
```

## Instalacja

Zainstalowanie projektu jest trochę wymagające ponieważ Jonas oparł go na tak zwanym "Legacy Code", co niestety jeżeli użyjemy flagi pozwalającego zainstalowanie kodu który został wycofany `sudo npm install --legacy-peer-deps` spowoduje, że nowsza wersja `node.js` wywali błąd.

Dlatego aby naprawić aktualne zależności należy przejść kroki:

1. instalacja narzędzia, które pozwoli na zaktualizowanie zależności w pliku package.json `sudo npm install -g npm-check-updates`
2. uruchomienie `npm-check-updates` za pomocą komendy `ncu`
3. zaktualizowanie pliku `package.json` do znalezionych wersji za pomocą komendy `ncu -u`
4. zainstalowanie zaktualizowanych pakietów `npm install` może być wymagana instalacja za pomocą `sudo npm install`

Jeżeli występuje nadal problem z instalacją projektu to należy użyć komendy:
`sudo npm install --force` - komenda wymusi instalację nowych zależności.

Jeżeli po instalacji i uruchomieniu projektu pojawi się nam bład w przeglądarce:

```
[eslint] EACCES: permission denied, mkdir '/<ścieżka_do_folderu_z_projektem>/node_modules/.cache'
```
To oznacza, że folder `node_modules` wymaga uprawnień administratora aby dokonywać w nim zmiany, aby naprawić taki bład należy wykonać komendę:

`sudo chmod -R 777 /<ścieżka_do_folderu_z_projektem>/` - to pozwoli nam na upewnienie się, że każdy plik jest dostępny dla każdego programu.