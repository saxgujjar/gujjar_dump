main.cpp
	contains initialization of MFC and commmands.

brepselect.cpp
	contains BrepEntity selections
		adcgGetBrBrep
		adcgGetBrFace
		adcgGetBrEdge
		adcgGetBrLoop
		adcgGetBrVertex

		adcgHighlightLoop
		selectPoint

breptrav.cpp
	provides the traversing and information functions

	travBrep(AcBrBrep* pBrep,CTreeCtrl& tree)
	travBrepComplexes(AcBrBrep* pBrep,CTreeCtrl& tree)
	travBrepEdges(AcBrBrep* pBrep,CTreeCtrl& tree)
	travBrepShells(AcBrBrep* pBrep,CTreeCtrl& tree)
	travBrepVertices(AcBrBrep* pBrep,CTreeCtrl& tree)

	travComplexShell(AcBrBrep* pBrep,CTreeCtrl& tree,HTREEITEM after)

	travEdgeLoop(AcBrEdge* pEdge,CTreeCtrl& tree)
	travFaceLoop(AcBrFace* pFace,CTreeCtrl& tree,HTREEITEM after)
	travLoopEdge(AcBrLoop* pLoop,CTreeCtrl& tree,HTREEITEM after)
	travLoopVertex(AcBrLoop* pLoop,CTreeCtrl& tree)
	travShellFace(AcBrShell* pShell,CTreeCtrl& tree,HTREEITEM after)
	travVertexEdges(AcBrVertex* pVertex,CTreeCtrl& tree)
	travVertexLoops(AcBrVertex* pVertex,CTreeCtrl& tree)

	adcgAcBrFaceInfo(const AcBrFace* pFace,strstream& s,BOOL highlight)
	adcgAcBrLoopInfo(const AcBrLoop* pLoop,strstream& s,BOOL highlight)
	adcgAcBrEdgeInfo(const AcBrEdge* pEdge,strstream& s,BOOL highlight)
	adcgAcBrVertexInfo(const AcBrVertex* pVertex,strstream& s,BOOL highlight)
	adcgGetBoundBlock(AcBrEntity* pBrEnt,strstream& s)

MfcBrepTravDlg.cpp
	is the MFC interface for the user

toolfunc.cpp
	adcgGetSubentPath	
		get an AcDbFullSubentPath from a resbuf list obtained by
		ads_ssnamex

	adcgErrorMsg 
		print an error message

	adcgGetLinearEnt
		get a linear entity (AcDbLine, AcDbXLine or AcDbRay)
		trough user selection

	adcgGetYesOrNo
		get a "Yes" or "No" from the user

	drawInfo
		(const AcGePoint3d& p1, const AcGePoint3d& p2,short color=3)
			draw a line with ads_grdraw
		(const AcGePoint3d& pWcs,short color=3)
			draw a point
		(const AcGePoint3dArray& ar,short color = 3)
			draw a polygon
		(const AcGeBoundBlock3d& block,short color = 3)
			draw a bounding box
		(const AcGeCurve3d* crv,short color = 3)
			draw any AcGeCurve3d

	AcDbEntity* selectEntity(const char* prompt, AcDbObjectId& id, 
		AcGePoint3d& pick,AcDb::OpenMode openMode )

	wait()
		wait until the user presses any key