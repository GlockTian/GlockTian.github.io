---
layout: post
title: "About two way binding in blazor"
subtitle: "A usage of two way binding in one my project experience"
date: 2021-12-18 10:09:13 -0400
background: '/img/posts/02.jpg'
tags: [Olympic, C#, web]
---

Q: Why happened? Why do I need it in the project?

A: We were trying to control a object that is reference in the child component

Child

```wasm
@using System.Net.Http.Json
@using MudBlazor.Examples.Data.Models
@inject HttpClient httpClient

<MudTable @ref="_table" Items="@Elements.Take(4)" Loading="@_loading" LoadingProgressColor="Color.Info">
    <HeaderContent>
        <MudTh>Name</MudTh>
        <MudTh>Molar mass</MudTh>
    </HeaderContent>
    <RowTemplate>
        <MudTd DataLabel="Name">@context.Name</MudTd>
        <MudTd DataLabel="Molar mass">@context.Molar</MudTd>
    </RowTemplate>
</MudTable>

<MudButton OnClick="async ()=>await load()">Refresh</MudButton>

@code {
    private bool _loading =true;
    private IEnumerable<Element> Elements = new List<Element>();
    private MudTable<Element> _table;
    protected override async Task OnInitializedAsync()
    {
        await load();
    }
    protected async Task load(){
				if(_table!=null)
            _table.SetEditingItem(null);
        _loading = true;
        Elements = await httpClient.GetFromJsonAsync<List<Element>>("webapi/periodictable");
        _loading = false;
    }
}
```

Parent:

```wasm
<Child></Child>

@code{
// parent logic
}
```

It becomes a requirement that we need to refresh the table in Child when some events occur in the parent.

Note that passing a parameter normally will not solve the problem becuase MudTable is a complex type. Two way binding is necessary in this case, if the parent want to access the _table reference in the Child.

Therefore we have: 

from this post [https://stackoverflow.com/questions/57932850/how-to-make-two-way-binding-on-blazor-component](https://stackoverflow.com/questions/57932850/how-to-make-two-way-binding-on-blazor-component)

Child

```wasm
@using System.Net.Http.Json
@using MudBlazor.Examples.Data.Models
@inject HttpClient httpClient

<MudTable @ref="_table" Items="@Elements.Take(4)" Loading="@_loading" LoadingProgressColor="Color.Info">
    <HeaderContent>
        <MudTh>Name</MudTh>
        <MudTh>Molar mass</MudTh>
    </HeaderContent>
    <RowTemplate>
        <MudTd DataLabel="Name">@context.Name</MudTd>
        <MudTd DataLabel="Molar mass">@context.Molar</MudTd>
    </RowTemplate>
</MudTable>

<MudButton OnClick="async ()=>await load()">Refresh</MudButton>

@code {
    private bool _hidePosition;
    private bool _loading =true;
    private IEnumerable<Element> Elements = new List<Element>();

    private MudTable<Element> _table;

    [Parameter]
    public MudTable<Element> Table
    {
        get => _table;
        set
        {
            if (_table == value ) return;
            _table = value;
            BindingValueChanged.InvokeAsync(value);
        }
    }

    [Parameter]
    public EventCallback<MudTable<Element>> BindingValueChanged { get; set; }
    protected override async Task OnInitializedAsync()
    {
        await load();
    }
    protected async Task load(){
				if(_table!=null)
            _table.SetEditingItem(null);
        _loading = true;
        Elements = await httpClient.GetFromJsonAsync<List<Element>>("webapi/periodictable");
        _loading = false;
    }
}
```

Parent:

```wasm
<Child @bind-Table="Table"></Child>

@code{
			protected MudTable<Element> Table;
			// parent logic
			protected async Task RefreshTable(){
				if(_table!=null)
            _table.SetEditingItem(null);
	    }
		
}
```

This we can reset the editing mode and everyone is happy