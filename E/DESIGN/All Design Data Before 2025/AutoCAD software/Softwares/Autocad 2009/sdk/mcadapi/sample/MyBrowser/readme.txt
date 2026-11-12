Question :
How to integrate with the Mechanical Desktop Browser

Answer :

With Mechanical Desktop 4 we have to take care about multiple documents. 
Within some documents the user may have activated a custom browser
dialog and on some not. Whenever a document is closed we have to take care
that we clean up our custom browser dialog. In order to manage custom browser
dialogs within multiple documents you may use the method the ObjectARX Wizard
provides. This sample was created with the ObjectARX Wizard. The Wizard creates
the file DocData.cpp, DocData.h and AsdkMgr.h

This sample adds new member variables
	CMyBrowserDlg*	m_pDlg;	// pointer to the custom browser dialog
	AcApDocument	m_pDoc;	// Documment where dialog resides

and new member functions
	AmiStatus addBrowser();		// To add a new browser dialog
	AmiStatus removeBrowser();	// To remove the browser dialog

in class CDocData (DocData.h)

The command adcgAddBrowser creates a new browser tab into the current document.
To do this we use the CDocData
		DocVars.docData().addBrowser();

Adding an own browser tab is done :
	1. Make sure that you use the right resource
			CAcModuleResourceOverride resOverride;
	2. Create the dialog as modeless dialog !
			m_pDlg = new CMyBrowserDlg()
			m_pDlg->Create(..)
	3. Add the new dialog to the browser
			amiAddBrowserTab

Removing the browser tab is done by
	amiRemoveBrowserTab(m_pDlg,m_pDoc)

Within the destructor of CDocData we remove the custom browser tab by calling our CDocData function
	removeBrowser()
which removes the tab and destroys the window.

Otherwise we don't have to take care about any document states or how many
documents with our browser exits. The destructor of CDocData is called automatically
if a document is destroyed.


Design your dialog with the resource editor. 
Make sure that you set "Child" as Style. Turn the title bar off
and set the border to none.

Implement an ON_WM_SIZE member function in order to adjust your
dialog to the size of the browser.

Implement an OnDestroy member function if you need to clean up
your dialog.

For right mouse button menus implement an ON_WM_CONTEXTMENU function.

If you want to highlight entities you show in the dialog you may
add hook to mouse messages. 

The attached sample has a CTreeCtrl inside the dialog and displays
the assembly structure. If you move with the mouse inside the
browser window the selected component will be highlighted. As soon
as the mouse moves outside the window the component will be 
unhighlighted. Since the highlighted objects are differently in different
documents we store the mouse hook variables also in the CDocData class.

If you need to know whether the browser is visible you can call  amiIsBrowserDisplayed()

This sample doesn't react to any new components the user may create !!

Testing your application :

1. Start a single drawing document
1.1 Call the command which adds your browser tab
1.2 Unload your application ( Does the browser tab remove correctly )

2. Start a single drawing document
2.1 Call the command which adds your browser tab
2.2 Close the document ( Do you clean up correctly )

3. Create multiple drawing documents and add your browser to each document
3.1 Unload you application

4. Create multiple drawing documents and add your browser to each document 
4.1 Exit AutoCAD
