# MASSVOIDTOOL — CLAUDE SESSION TRANSFER DOSSIER

Generated from the latest development ZIP supplied by the user.
Purpose: provide Claude with a text-only reconstruction because the ZIP cannot be uploaded directly.

IMPORTANT: This dossier is a text reconstruction, not a substitute for a byte-level package audit. The exact latest diagnostic source is included below. Locked-file hashes are included so Claude can compare if the source is later pasted separately.

## 1. CURRENT INVESTIGATION GOAL

Investigate why an Adaptive Family can receive a rotated Adaptive Point coordinate system / position, while only part of the family geometry visually responds instead of the whole family becoming a rigidly rotated panel like a rotated Divided Surface cell.

Desired behavior: rotating one quadrilateral cell by 45 degrees should rotate the whole panel geometry, producing a diagonal / diamond-like orientation.

Do NOT modify production rotation code until the construction dependency/root cause is established.

## 2. ESTABLISHED FACTS

- Family under investigation: Tinggi Kaki.
- Category: Curtain Panels.
- FamilyPlacementType raw: OneLevelBased.
- Runtime enum contains Adaptive.
- IsAdaptiveComponentFamily(OwnerFamily) = TRUE.
- GetNumberOfAdaptivePoints(OwnerFamily) = 4.
- Four Adaptive Placement Points exist.
- All four points were previously verified as ToHostAndLoopSystem.
- Adaptive Point coordinate frames can be changed successfully with mathematically valid orthonormal frames.
- Adaptive Point positions can also be moved.
- Visual testing shows the Tinggi Kaki geometry does NOT always behave as one rigid body under those changes: some geometry responds, while other geometry remains in the previous orientation.
- A direct corner-position rotation experiment also moved the adaptive points to a true 45-degree quadrilateral, but did not make all family geometry behave like a rotated Divided Surface panel.
- Therefore, do NOT reduce the problem to SetCoordinateSystem() alone.

## 3. IMPORTANT PREVIOUS EVIDENCE

Previous family construction diagnostics found:
- 5 Forms: 567395, 567416, 567552, 567668, 567714.
- 0 ReferencePlane elements were reported by the diagnostic.
- 91 Dimensions.
- 33 FamilyParameters.
- Sketch.SketchPlaneId is not available on this Revit runtime.
- Previous GetDependentElements()+BFS investigation is considered insufficient for orientation dependency and MUST NOT be repeated as the primary method.
- One prior Form (567552) was the only Form without evidence of POSITION/EXISTENCE dependency to adaptive points in that previous graph. This is not proof of orientation independence.

Dimension topology already observed in an earlier run:
Point 567312 was referenced by dimensions: 567406, 567407, 567443, 567647, 567648, 567698, 567699.
Point 567313: 567410, 567411, 567455, 567657, 567658, 567701, 567702.
Point 567314: 567412, 567413, 567454, 567588, 567589, 567704, 567705.
Point 567315: 567408, 567409, 567451, 567707, 567708.
These are real Dimension.Reference evidence, but the causal role of those dimensions in the rotation problem is NOT established.

## 4. LOCKED FILES

Do not modify:
- mass_panel_core.py
- mass_panel_rotation.py
- mass_panel_storage.py
- mass_panel_storage_v5.py

Baseline SHA-256 from the current package:
- mass_panel_core.py = b766805383f1e03242b3341fd9ba7821abc1cca226bd83cd7d27f818b01d18cd
- mass_panel_rotation.py = 545c8a7c51acad95327eff502a0dc9795d8f02963c7c789dce48594352625805
- mass_panel_storage.py = f4a16a4549979a8c689716ea0fd2329ff5293507c50fec39989d0b0cdc850d60
- mass_panel_storage_v5.py = e6d5a709f93f313ebc3b447c230e4469db086002677b178eee639ef3ea4dd609

## 5. CURRENT PACKAGE MANIFEST

MassVoidTool_RotationDev.extension/MassVoidToolDev.tab/RotationDiagnostics.panel/AdaptiveFamilyConstructionDiagnostic.pushbutton/script.py
SIZE=68709 bytes
SHA256=b0f9b25b249c5bb2c6bdd5cfbb7a2b0b608bc5e3e69ada01d0e9f551bd4aedca

MassVoidTool_RotationDev.extension/MassVoidToolDev.tab/RotationDiagnostics.panel/AdaptiveFamilyGeometryDependencyDiagnostic.pushbutton/script.py
SIZE=41307 bytes
SHA256=48bbad137cfd820b0c28d38849c9a8e2766cc5d467699b608286596c81b853b4

MassVoidTool_RotationDev.extension/MassVoidToolDev.tab/RotationDiagnostics.panel/AdaptiveFormConstructionChainDiagnostic.pushbutton/script.py
SIZE=43000 bytes
SHA256=ef19ae9384f94318df7b904b6004f7959a8b63f6b60014570ecb0f1570166bb9

MassVoidTool_RotationDev.extension/lib/mass_panel_storage_v5.py
SIZE=10422 bytes
SHA256=e6d5a709f93f313ebc3b447c230e4469db086002677b178eee639ef3ea4dd609

MassVoidTool_RotationDev.extension/lib/mass_panel_rotation.py
SIZE=5828 bytes
SHA256=545c8a7c51acad95327eff502a0dc9795d8f02963c7c789dce48594352625805

MassVoidTool_RotationDev.extension/lib/mass_panel_core.py
SIZE=7342 bytes
SHA256=b766805383f1e03242b3341fd9ba7821abc1cca226bd83cd7d27f818b01d18cd

MassVoidTool_RotationDev.extension/lib/mass_panel_storage.py
SIZE=11124 bytes
SHA256=f4a16a4549979a8c689716ea0fd2329ff5293507c50fec39989d0b0cdc850d60

## 6. CURRENT DIAGNOSTIC SET

The package contains these three diagnostic pushbuttons:
1. AdaptiveFamilyConstructionDiagnostic
2. AdaptiveFamilyGeometryDependencyDiagnostic
3. AdaptiveFormConstructionChainDiagnostic

The current investigation should continue from these diagnostics rather than rebuilding earlier experiments.

## 7. CURRENT LATEST DIAGNOSTIC

AdaptiveFormConstructionChainDiagnostic was created specifically to avoid GetDependentElements(). It uses two different evidence routes:

A. CLR reflection on Sketch / GenericForm / FreeFormElement / ReferencePoint to discover real runtime properties/methods.
B. Direct attribute chains such as Curve.Reference.ElementId and Dimension.References.

It also contains a clearly labeled heuristic spatial BBox comparison, which must never be treated as verified construction linkage.

It is read-only, opens no Transaction, does not write storage/schema, and does not call rotation/write/delete APIs.

## 8. REQUIRED WORK PROTOCOL FOR CLAUDE

STEP 1 — audit the text dossier and the supplied source content.
STEP 2 — report exactly what is known, unknown, and missing.
STEP 3 — propose the next diagnostic, with exact evidence it will collect.
STOP. Do not code until the user explicitly approves the plan.

After approval:
- create exactly the planned diagnostic only;
- py_compile + AST all Python files;
- verify locked-file hashes unchanged;
- verify old diagnostics unchanged;
- grep for prohibited API calls;
- verify no storage/schema/production integration;
- package and stop for Revit runtime test.

IronPython 2.7: avoid nested comprehension/generator scoping. Prefer explicit loops.
If an API signature is uncertain, use reflection first. If unavailable, report UNKNOWN. Never guess.

Prohibited unless explicitly authorized as a separate experiment:
RotateElement, CreateRotation, CreateRotationAtPoint, SetCoordinateSystem, SetPointOrientationType, SetPointConstraintType, MakeAdaptivePoint, Delete, GetDependentElements.

## 9. LATEST SOURCE — AdaptiveFormConstructionChainDiagnostic/script.py

The exact source currently present in the supplied ZIP follows.

```python
# -*- coding: utf-8 -*-
"""
Adaptive Form Construction Chain Diagnostic
------------------------------------------------------------------
TUJUAN -- SATU dan HANYA SATU

AdaptiveFamilyConstructionDiagnostic (sesi lalu, GetDependentElements()
+ BFS) sudah menghasilkan evidence VERIFIED pada family "Tinggi Kaki":

    IsAdaptiveComponentFamily(OwnerFamily) = True
    GetNumberOfAdaptivePoints(OwnerFamily) = 4
    4 Adaptive Placement Point, Placement Number 1-4,
        PointOrientationType = ToHostAndLoopSystem (semua 4)
    5 Form: 567395, 567416, 567552, 567668, 567714
    Form 567552 = satu-satunya TANPA evidence POSITION/EXISTENCE
        dependency ke Adaptive Point (via GetDependentElements()/BFS)
    0 ReferencePlane ditemukan
    Sketch.SketchPlaneId TIDAK TERSEDIA pada runtime ini (AttributeError)
    91 Dimension, 33 FamilyParameter

Instruksi eksplisit sesi ini: **JANGAN mengulang GetDependentElements()**.
Tool ini TIDAK memanggil Element.GetDependentElements() sama sekali, di
mana pun. Sebagai gantinya, tool ini mencari evidence construction
chain lewat DUA jalur yang sepenuhnya berbeda dari sesi sebelumnya:

1. **Reflection murni terhadap CLR type Autodesk.Revit.DB.Sketch dan
   Autodesk.Revit.DB.GenericForm/FreeFormElement/ReferencePoint** --
   MENEMUKAN property/method apa yang BENAR-BENAR ada pada runtime ini
   (Sketch.SketchPlaneId TERBUKTI tidak ada di sesi lalu -- tool ini
   tidak lagi menebak nama property lain; ia mencetak SEMUA nama
   property/method yang benar-benar ditemukan reflection GetProperties()
   /GetMethods(), lalu mencoba setiap salah satu yang relevan (nama
   mengandung Plane/Profile/Sketch/Curve/Reference/Host) via getattr()
   langsung pada instance yang sudah ada -- IronPython mengekspos
   public CLR member sebagai atribut Python secara native, jadi getattr()
   pada instance real TIDAK membutuhkan System.Reflection.Invoke() manual
   seperti method static AdaptiveComponentFamilyUtils sebelumnya).

2. **Direct attribute chain**: Curve.Reference.ElementId pada setiap
   curve profile Sketch (attribute langsung, BUKAN GetDependentElements)
   dibandingkan langsung terhadap ElementId dari 4 Adaptive Placement
   Point yang sudah teridentifikasi -- serta Dimension.References
   (attribute langsung) dibandingkan dengan Point/Sketch/Form yang
   ditemukan. Kedua jalur ini adalah PROPERTY/ATTRIBUTE ACCESS biasa,
   bukan dependency-graph API, jadi sama sekali tidak "mengulang"
   investigasi GetDependentElements() sesi lalu.

Kalau reflection TIDAK menemukan property/method yang menghubungkan
Form secara langsung ke Sketch tertentu (sangat mungkin terjadi --
linkage Form<->Sketch di Revit API historically hanya terekspos lewat
dependency graph, yang sengaja TIDAK dipakai di sini), tool ini
menyediakan SATU evidence tambahan yang secara eksplisit dilabeli
HEURISTIC/DERIVED (bukan VERIFIED API EVIDENCE): korelasi spasial
BoundingBox Form vs BoundingBox kumpulan curve Sketch (solid yang
dibentuk oleh sebuah profile hampir selalu overlap secara spasial
dengan profile pembentuknya). Ini murni geometri (pakai titik yang
sudah didapat dari Solid/Curve, tidak ada API dependency call apa
pun), dan HANYA dipakai untuk comparison/HYPOTHESES, tidak pernah
diklaim sebagai VERIFIED link.

Tool ini TIDAK menggantikan, TIDAK mewarisi kode dari, dan TIDAK
memodifikasi diagnostic mana pun sebelumnya. Berdiri sendiri,
sepenuhnya terpisah.

------------------------------------------------------------------
LOCKED FILES -- HANYA fungsi baca-nama yang dipanggil apa adanya
------------------------------------------------------------------
    mass_panel_core.py  (get_family_name, get_type_name -- HANYA
                          dipakai untuk memilih family di mode Project
                          Document)

mass_panel_rotation.py, mass_panel_storage.py, mass_panel_storage_v5.py
TIDAK di-import sama sekali. Tidak ada Extensible Storage dibaca/
ditulis, tidak ada Schema/Entity apa pun.

------------------------------------------------------------------
READ-ONLY GUARANTEE
------------------------------------------------------------------
TIDAK PERNAH memanggil: ElementTransformUtils.RotateElement(),
Transform.CreateRotation()/CreateRotationAtPoint(),
ReferencePoint.SetCoordinateSystem(),
AdaptiveComponentFamilyUtils.SetPointOrientationType()/
SetPointConstraintType()/MakeAdaptivePoint(), Document.Delete()/
Element.Delete(), atau Element.GetDependentElements() (SENGAJA, per
instruksi sesi ini). TIDAK membuat, menghapus, atau mengubah geometry,
ReferencePlane, Sketch, parameter, atau elemen family apa pun.

Family document dibuka dengan cara yang sama seperti diagnostic
sebelumnya: kalau document aktif sudah Family Document, dipakai
langsung; kalau Project Document, dibuka via Document.EditFamily()
(in-memory, TIDAK PERNAH disimpan/di-load-back), SELALU ditutup tanpa
disimpan (Close(False)) di blok finally.

Tool ini TIDAK membuka Transaction sama sekali -- semua operasi di
sini (reflection GetProperties()/GetMethods(), getattr() pada
instance, pembacaan Solid/Curve/Dimension) adalah pure-read, tidak
pernah membutuhkan Transaction terbuka (berbeda dari
GetDependentElements() pada diagnostic sebelumnya, yang historically
butuh Transaction -- API tersebut TIDAK dipakai di sini sama sekali).

------------------------------------------------------------------
OUTPUT STRUCTURE
------------------------------------------------------------------
=== VERIFIED API EVIDENCE ===
=== UNKNOWN / API LIMITATION ===
=== COMPARISON BETWEEN FORMS ===
=== HYPOTHESES ===

Tidak ada PASS/FAIL. Tidak ada root-cause final. HEURISTIC/DERIVED
evidence (korelasi spasial) TIDAK PERNAH muncul di VERIFIED API
EVIDENCE -- hanya di COMPARISON BETWEEN FORMS (diberi label eksplisit)
dan HYPOTHESES.
"""

import System
import clr
from pyrevit import revit, DB, forms, script
from System.Reflection import BindingFlags

from mass_panel_core import get_family_name, get_type_name

doc = revit.doc
uidoc = revit.uidoc
output = script.get_output()

output.print_md("## Adaptive Form Construction Chain Diagnostic")
output.print_md(
    "Read-only, development-only. TIDAK memanggil Element.GetDependentElements() sama "
    "sekali (per instruksi sesi ini). Evidence datang dari reflection CLR + direct "
    "attribute access (Curve.Reference, Dimension.References) saja. TIDAK ADA geometry/"
    "family/parameter yang dibuat, dihapus, atau diubah. TIDAK ADA PASS/FAIL, TIDAK ADA "
    "root-cause final.")


# ==================================================================
# Generic read-only helpers.
# ==================================================================
def fmt_eid(eid):
    if eid is None:
        return "None"
    try:
        return str(int(eid.Value))
    except Exception:
        pass
    try:
        return str(int(eid.IntegerValue))
    except Exception:
        pass
    return str(eid)


def fmt_xyz(p):
    if p is None:
        return "None"
    try:
        return "({:.6f}, {:.6f}, {:.6f})".format(p.X, p.Y, p.Z)
    except Exception:
        return str(p)


def safe_attr(obj, name):
    try:
        return getattr(obj, name), None
    except Exception as ex:
        return None, "{}: {}".format(type(ex).__name__, ex)


def safe_call(fn):
    try:
        return fn(), None
    except Exception as ex:
        return None, "{}: {}".format(type(ex).__name__, ex)


def clr_full_name(py_type):
    try:
        t = clr.GetClrType(py_type)
        full_name, _ = safe_attr(t, "FullName")
        return full_name, t, None
    except Exception as ex:
        return None, None, "{}: {}".format(type(ex).__name__, ex)


# ==================================================================
# Reflection ground-truth: discover REAL property/method names on a
# CLR type -- never assumed, never hardcoded from prior sessions.
# ==================================================================
def reflect_member_names(py_type):
    """Return (property_names_sorted, method_names_sorted, clr_type, err)."""
    full_name, clr_type, err = clr_full_name(py_type)
    if err or clr_type is None:
        return [], [], None, err
    flags = BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.Instance
    try:
        props = sorted(set(p.Name for p in clr_type.GetProperties(flags)))
    except Exception as ex:
        props = []
    try:
        methods = sorted(set(m.Name for m in clr_type.GetMethods(flags)))
    except Exception as ex:
        methods = []
    return props, methods, clr_type, None


RELEVANT_KEYWORDS = ["plane", "profile", "sketch", "curve", "reference", "host", "owner", "loop"]


def is_relevant_name(name):
    lname = name.lower()
    return any(k in lname for k in RELEVANT_KEYWORDS)


def dump_relevant_members(obj, property_names):
    """For a live instance obj, try getattr(obj, name) for every
    reflection-discovered property name that looks relevant (see
    RELEVANT_KEYWORDS). Plain getattr() -- IronPython exposes public
    CLR instance members as Python attributes natively, no manual
    System.Reflection.Invoke() needed for instance property access.
    Returns list of (name, value_repr, err)."""
    results = []
    for name in property_names:
        if not is_relevant_name(name):
            continue
        value, err = safe_attr(obj, name)
        if err:
            results.append((name, None, err))
        else:
            results.append((name, value, None))
    return results


# ==================================================================
# STEP 0: Obtain a Family Document (same pattern as prior diagnostics).
# ==================================================================
family_doc_opened_here = False
work_doc = None

if doc.IsFamilyDocument:
    work_doc = doc
    output.print_md("\n**Mode: document aktif SUDAH Family Document** -- dipakai langsung.")
else:
    output.print_md("\n**Mode: document aktif adalah Project Document** -- tool akan membuka "
                     "SATU Adaptive Family via Document.EditFamily() (in-memory, read-only).")
    candidates = DB.FilteredElementCollector(doc).OfClass(DB.FamilySymbol).ToElements()
    family_map = {}
    for sym in candidates:
        try:
            if sym.Family.FamilyPlacementType != DB.FamilyPlacementType.Adaptive:
                continue
        except Exception:
            continue
        fam_name = get_family_name(sym)
        if fam_name not in family_map:
            family_map[fam_name] = sym.Family
    if not family_map:
        forms.alert("Tidak ada Adaptive Family yang loaded di project ini.",
                     title="Tidak ada Adaptive Family", exitscript=True)
    fam_labels = sorted(family_map.keys())
    chosen_fam_label = forms.SelectFromList.show(
        fam_labels, title="PILIH Adaptive Family (mis. 'Tinggi Kaki') -- Anda yang menentukan",
        button_name="Buka di Family Editor (read-only)", multiselect=False)
    if chosen_fam_label is None:
        script.exit()
    target_family = family_map[chosen_fam_label]
    output.print_md("Family dipilih: **{}**".format(chosen_fam_label))
    try:
        work_doc = doc.EditFamily(target_family)
        family_doc_opened_here = True
    except Exception as ex:
        output.print_md("**GAGAL membuka family: {}**".format(ex))
        script.exit()
    output.print_md("Family document dibuka in-memory via EditFamily() -- TIDAK disimpan, "
                     "akan ditutup Close(False) di akhir.")

verified_evidence = []
unknown_items = []

try:
    if not work_doc.IsFamilyDocument:
        output.print_md("\n**STOP -- bukan Family Document.**")
        script.exit()

    owner_family, owner_err = safe_attr(work_doc, "OwnerFamily")
    if owner_err or owner_family is None:
        output.print_md("\n**STOP -- OwnerFamily FAILED ({})**".format(owner_err))
        script.exit()

    # ==============================================================
    # Minimal re-verification (single calls, NOT a full re-audit) of
    # the two facts already established last session, using the SAME
    # reflection-verified-signature engine (not GetDependentElements).
    # ==============================================================
    output.print_md("\n---\n### Quick re-verification (single reflection-verified calls)")

    full_name, acfu_clr_type, clr_err = clr_full_name(DB.AdaptiveComponentFamilyUtils)
    all_method_infos = []
    if not clr_err and acfu_clr_type is not None:
        try:
            flags = BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.Static | BindingFlags.Instance
            all_method_infos = list(acfu_clr_type.GetMethods(flags))
        except Exception as ex:
            unknown_items.append("AdaptiveComponentFamilyUtils.GetMethods() failed: {}".format(ex))

    def resolve_arg_for_param(p, point_id):
        try:
            type_full = p.ParameterType.FullName or ""
        except Exception as ex:
            return None, False, "ParameterType.FullName FAILED: {}".format(ex)
        if type_full == "Autodesk.Revit.DB.Document":
            return work_doc, True, "work_doc"
        if type_full == "Autodesk.Revit.DB.Family":
            return owner_family, True, "owner_family"
        if type_full == "Autodesk.Revit.DB.ElementId":
            if point_id is not None:
                return point_id, True, "point_id"
            return None, False, "ElementId param but no point_id supplied"
        return None, False, "no known runtime object for type '{}'".format(type_full)

    def build_args_for(method_info, point_id=None):
        try:
            params = list(method_info.GetParameters())
        except Exception as ex:
            return None, "GetParameters() FAILED: {}".format(ex)
        args = []
        for p in params:
            value, ok, info = resolve_arg_for_param(p, point_id)
            if not ok:
                return None, info
            args.append(value)
        return args, None

    def invoke_via_reflection(method_info, args):
        try:
            net_args = System.Array[System.Object](args) if args else System.Array[System.Object](0)
            result = method_info.Invoke(None, net_args)
            return result, None
        except Exception as ex:
            inner = getattr(ex, "InnerException", None)
            if inner is not None:
                return None, "{}: {}".format(type(inner).__name__, inner)
            return None, "{}: {}".format(type(ex).__name__, ex)

    def call_first_success(method_name, point_id=None):
        matches = [m for m in all_method_infos if m.Name == method_name]
        for m in matches:
            args, skip_reason = build_args_for(m, point_id)
            if skip_reason:
                continue
            value, err = invoke_via_reflection(m, args)
            if err is None:
                return value, None
        return None, "no successful overload (method not available, or all attempts SKIPPED/FAILED)"

    iacf_value, iacf_err = call_first_success("IsAdaptiveComponentFamily")
    output.print_md("- IsAdaptiveComponentFamily(OwnerFamily) = **{}**".format(
        iacf_value if iacf_err is None else "UNKNOWN ({})".format(iacf_err)))
    if iacf_err is None:
        verified_evidence.append("IsAdaptiveComponentFamily(OwnerFamily) = {}".format(iacf_value))

    n_adaptive_value, n_adaptive_err = call_first_success("GetNumberOfAdaptivePoints")
    output.print_md("- GetNumberOfAdaptivePoints(OwnerFamily) = **{}**".format(
        n_adaptive_value if n_adaptive_err is None else "UNKNOWN ({})".format(n_adaptive_err)))
    if n_adaptive_err is None:
        verified_evidence.append("GetNumberOfAdaptivePoints(OwnerFamily) = {}".format(n_adaptive_value))

    # ==============================================================
    # Identify the CONFIRMED Adaptive Placement Points (foundational
    # identification -- NOT a repeat of the dependency/BFS
    # investigation; uses IsAdaptivePoint/IsAdaptivePlacementPoint/
    # GetPlacementNumber/GetPointOrientationType only).
    # ==============================================================
    output.print_md("\n### Confirmed Adaptive Placement Points (identification only)")

    all_ref_points, rp_err = safe_call(
        lambda: list(DB.FilteredElementCollector(work_doc).OfClass(DB.ReferencePoint)))
    all_ref_points = all_ref_points or []
    output.print_md("FilteredElementCollector found {} ReferencePoint element(s) total.".format(len(all_ref_points)))

    confirmed_points = []  # list of dict: id, placement_number, position, orientation_type
    for pt_el in all_ref_points:
        pt_id = pt_el.Id
        is_placement, _ = call_first_success("IsAdaptivePlacementPoint", point_id=pt_id)
        is_flagged = False
        try:
            is_flagged = bool(is_placement)
        except Exception:
            is_flagged = False
        if not is_flagged:
            continue
        placement_number, pn_err = call_first_success("GetPlacementNumber", point_id=pt_id)
        orient_value, orient_err = call_first_success("GetPointOrientationType", point_id=pt_id)
        position, pos_err = safe_attr(pt_el, "Position")
        confirmed_points.append({
            "id": pt_id, "id_str": fmt_eid(pt_id),
            "placement_number": placement_number if pn_err is None else None,
            "position": position if not pos_err else None,
            "orientation_type": orient_value if orient_err is None else None,
        })

    confirmed_points.sort(key=lambda e: (e["placement_number"] if e["placement_number"] is not None else 999))
    output.print_md("Confirmed via IsAdaptivePlacementPoint = **{}** point(s):".format(len(confirmed_points)))
    for cp in confirmed_points:
        output.print_md("- ElementId {} -- Placement Number = {}, Position = {}, OrientationType = {}".format(
            cp["id_str"], cp["placement_number"], fmt_xyz(cp["position"]), cp["orientation_type"]))
    verified_evidence.append("{} confirmed Adaptive Placement Point(s) via IsAdaptivePlacementPoint: {}".format(
        len(confirmed_points), ", ".join(cp["id_str"] for cp in confirmed_points)))

    confirmed_point_ids_str = set(cp["id_str"] for cp in confirmed_points)

    # ==============================================================
    # Reflection ground-truth: Sketch, GenericForm, FreeFormElement,
    # ReferencePoint CLR member names -- ACTUAL names on this runtime.
    # ==============================================================
    output.print_md("\n---\n### === VERIFIED API EVIDENCE ===")
    output.print_md("#### Reflection: real CLR member names on THIS runtime (ground truth, not assumed)")

    type_targets = [
        ("Autodesk.Revit.DB.Sketch", DB.Sketch),
        ("Autodesk.Revit.DB.GenericForm", DB.GenericForm),
        ("Autodesk.Revit.DB.ReferencePoint", DB.ReferencePoint),
    ]
    try:
        type_targets.append(("Autodesk.Revit.DB.FreeFormElement", DB.FreeFormElement))
    except Exception:
        pass

    reflected_props = {}  # full_name -> property_names_sorted
    for label, py_type in type_targets:
        props, methods, clr_type, err = reflect_member_names(py_type)
        if err:
            output.print_md("- **{}**: reflection FAILED ({})".format(label, err))
            unknown_items.append("Reflection on {} failed: {}".format(label, err))
            continue
        reflected_props[label] = props
        output.print_md("- **{}**: {} propert(y/ies), {} method(s) found.".format(label, len(props), len(methods)))
        output.print_md("  Properties: {}".format(", ".join(props) if props else "(none)"))
        output.print_md("  Methods: {}".format(", ".join(methods) if methods else "(none)"))
        has_sketchplaneid = "SketchPlaneId" in props or "SketchPlaneId" in methods
        if label == "Autodesk.Revit.DB.Sketch":
            output.print_md("  SketchPlaneId present on this runtime = **{}** (confirms/refutes prior "
                             "session's finding directly via reflection, not by trial-and-error).".format(
                                 has_sketchplaneid))
            verified_evidence.append("Sketch CLR type on this runtime: SketchPlaneId present = {}".format(
                has_sketchplaneid))
            if not has_sketchplaneid:
                unknown_items.append("Sketch.SketchPlaneId is confirmed NOT PRESENT on this runtime's Sketch "
                                      "CLR type (reflection-verified, not just AttributeError-caught).")

    # ==============================================================
    # === SKETCHES -- reflection-driven relevant-member dump ===
    # ==============================================================
    output.print_md("\n#### Sketches -- relevant member dump (reflection-discovered names only)")

    sketches = list(DB.FilteredElementCollector(work_doc).OfClass(DB.Sketch))
    sketch_props = reflected_props.get("Autodesk.Revit.DB.Sketch", [])
    sketch_data = []
    for sk in sketches:
        sk_id_str = fmt_eid(sk.Id)
        member_dump = dump_relevant_members(sk, sketch_props)

        profile_curves = []
        profile, profile_err = safe_attr(sk, "Profile")
        if not profile_err and profile is not None:
            try:
                for loop in profile:
                    for curve in loop:
                        c_ref, c_ref_err = safe_call(lambda cu=curve: cu.Reference)
                        c_id = None
                        if not c_ref_err and c_ref is not None:
                            try:
                                c_id = fmt_eid(c_ref.ElementId)
                            except Exception:
                                c_id = None
                        try:
                            start_pt = curve.GetEndPoint(0)
                            end_pt = curve.GetEndPoint(1)
                        except Exception:
                            start_pt = end_pt = None
                        profile_curves.append({"ref_id": c_id, "start": start_pt, "end": end_pt,
                                                "curve_type": curve.GetType().Name})
            except Exception as ex:
                profile_err = "iteration FAILED: {}".format(ex)

        matched_point_ids = set(c["ref_id"] for c in profile_curves if c["ref_id"] in confirmed_point_ids_str)

        sketch_data.append({"id": sk_id_str, "element": sk, "member_dump": member_dump,
                             "profile_curves": profile_curves, "matched_point_ids": matched_point_ids})

        output.print_md("\n**Sketch {}**".format(sk_id_str))
        if member_dump:
            for name, value, err in member_dump:
                output.print_md("- {} = {}".format(name, value if err is None else "FAILED ({})".format(err)))
        else:
            output.print_md("- (no relevant-keyword property found via reflection on this runtime)")
        if profile_err:
            output.print_md("- Profile: FAILED ({})".format(profile_err))
        else:
            output.print_md("- Profile: {} curve(s), {} with Reference.ElementId matching a confirmed "
                             "Adaptive Point = {}".format(
                                 len(profile_curves), len(matched_point_ids),
                                 ", ".join(matched_point_ids) if matched_point_ids else "(none)"))
            if matched_point_ids:
                verified_evidence.append("Sketch {} has profile curve(s) whose Curve.Reference.ElementId "
                                          "directly matches confirmed Adaptive Point(s) {} (direct attribute "
                                          "evidence, NOT GetDependentElements)".format(
                                              sk_id_str, ", ".join(matched_point_ids)))

    if not sketches:
        output.print_md("No Sketch elements found.")
        unknown_items.append("No Sketch elements found in this family document.")

    # ==============================================================
    # === FORMS -- geometry + reflection-driven relevant-member dump ===
    # ==============================================================
    output.print_md("\n---\n### FORMS -- geometry + reflection-driven relevant-member dump")

    forms_elems = list(DB.FilteredElementCollector(work_doc).OfClass(DB.GenericForm))
    freeform_elems = []
    try:
        freeform_elems = list(DB.FilteredElementCollector(work_doc).OfClass(DB.FreeFormElement))
    except Exception:
        freeform_elems = []
    all_form_elems = list(forms_elems) + list(freeform_elems)
    genericform_props = reflected_props.get("Autodesk.Revit.DB.GenericForm", [])
    freeform_props = reflected_props.get("Autodesk.Revit.DB.FreeFormElement", [])

    def collect_solids(geometry_element):
        solids = []
        if geometry_element is None:
            return solids
        for obj in geometry_element:
            if isinstance(obj, DB.Solid):
                try:
                    if obj.Volume > 1e-9:
                        solids.append(obj)
                except Exception:
                    continue
            elif isinstance(obj, DB.GeometryInstance):
                try:
                    inst_geom = obj.GetInstanceGeometry()
                except Exception:
                    continue
                solids.extend(collect_solids(inst_geom))
        return solids

    def geometry_bbox_and_volume(elem):
        result = {"solid_count": 0, "total_volume": 0.0, "bbox_min": None, "bbox_max": None, "error": None}
        try:
            opts = DB.Options()
            opts.ComputeReferences = False
            opts.IncludeNonVisibleObjects = False
            opts.DetailLevel = DB.ViewDetailLevel.Fine
            geom = elem.get_Geometry(opts)
            if geom is None:
                result["error"] = "get_Geometry() returned None"
                return result
            solids = collect_solids(geom)
            result["solid_count"] = len(solids)
            all_pts = []
            total_vol = 0.0
            for s in solids:
                try:
                    total_vol += s.Volume
                except Exception:
                    pass
                try:
                    for e in s.Edges:
                        crv = e.AsCurve()
                        for pt in crv.Tessellate():
                            all_pts.append((pt.X, pt.Y, pt.Z))
                except Exception:
                    continue
            result["total_volume"] = total_vol
            if all_pts:
                xs = [p[0] for p in all_pts]
                ys = [p[1] for p in all_pts]
                zs = [p[2] for p in all_pts]
                result["bbox_min"] = (min(xs), min(ys), min(zs))
                result["bbox_max"] = (max(xs), max(ys), max(zs))
        except Exception as ex:
            result["error"] = str(ex)
        return result

    def bbox_overlap_fraction(bbox_a_min, bbox_a_max, bbox_b_min, bbox_b_max):
        """HEURISTIC ONLY. Returns fraction (0..1) of overlap volume relative
        to the smaller of the two boxes, or None if not computable. Purely
        geometric -- no API call involved."""
        if not (bbox_a_min and bbox_a_max and bbox_b_min and bbox_b_max):
            return None
        try:
            overlap_dims = []
            vol_a = 1.0
            vol_b = 1.0
            for k in range(3):
                lo = max(bbox_a_min[k], bbox_b_min[k])
                hi = min(bbox_a_max[k], bbox_b_max[k])
                overlap_dims.append(max(0.0, hi - lo))
                vol_a *= max(1e-9, bbox_a_max[k] - bbox_a_min[k])
                vol_b *= max(1e-9, bbox_b_max[k] - bbox_b_min[k])
            overlap_vol = overlap_dims[0] * overlap_dims[1] * overlap_dims[2]
            smaller = min(vol_a, vol_b)
            if smaller <= 1e-9:
                return None
            return overlap_vol / smaller
        except Exception:
            return None

    form_data = []
    for fe in all_form_elems:
        fe_id_str = fmt_eid(fe.Id)
        runtime_type = fe.GetType().Name
        gs = geometry_bbox_and_volume(fe)

        applicable_props = genericform_props if isinstance(fe, DB.GenericForm) else freeform_props
        member_dump = dump_relevant_members(fe, applicable_props)

        form_data.append({"id": fe_id_str, "element": fe, "runtime_type": runtime_type,
                           "geom": gs, "member_dump": member_dump})

        output.print_md("\n**Form {} ({})**".format(fe_id_str, runtime_type))
        if gs["error"]:
            output.print_md("- Geometry: FAILED ({})".format(gs["error"]))
        else:
            output.print_md("- Solid count = {}, Volume = {:.6f} ft3".format(gs["solid_count"], gs["total_volume"]))
            if gs["bbox_min"]:
                output.print_md("- BBox Min = {}, Max = {}".format(
                    "({:.6f}, {:.6f}, {:.6f})".format(*gs["bbox_min"]),
                    "({:.6f}, {:.6f}, {:.6f})".format(*gs["bbox_max"])))
        if member_dump:
            output.print_md("- Reflection-relevant members ({}):".format(runtime_type))
            for name, value, err in member_dump:
                output.print_md("  - {} = {}".format(name, value if err is None else "FAILED ({})".format(err)))
        else:
            output.print_md("- No relevant-keyword property found via reflection on this runtime "
                             "({} type has no direct Sketch/Profile/Reference-named member).".format(runtime_type))
            unknown_items.append("Form {} ({}): no reflection-discovered property links it directly to a "
                                  "Sketch/Profile.".format(fe_id_str, runtime_type))

    if not all_form_elems:
        output.print_md("No Form elements found.")

    # ==============================================================
    # Spatial correlation (HEURISTIC/DERIVED ONLY) between each Form's
    # BBox and each Sketch's profile-curve BBox -- NOT an API link.
    # ==============================================================
    output.print_md("\n---\n### Spatial correlation Form<->Sketch (HEURISTIC/DERIVED ONLY -- "
                     "pure geometry, NOT an API-confirmed link, NOT GetDependentElements)")

    for sd in sketch_data:
        pts = []
        for c in sd["profile_curves"]:
            if c["start"]:
                pts.append((c["start"].X, c["start"].Y, c["start"].Z))
            if c["end"]:
                pts.append((c["end"].X, c["end"].Y, c["end"].Z))
        if pts:
            xs = [p[0] for p in pts]
            ys = [p[1] for p in pts]
            zs = [p[2] for p in pts]
            sd["bbox_min"] = (min(xs), min(ys), min(zs))
            sd["bbox_max"] = (max(xs), max(ys), max(zs))
        else:
            sd["bbox_min"] = sd["bbox_max"] = None

    for fdta in form_data:
        best = None
        for sd in sketch_data:
            frac = bbox_overlap_fraction(fdta["geom"]["bbox_min"], fdta["geom"]["bbox_max"],
                                          sd.get("bbox_min"), sd.get("bbox_max"))
            if frac is not None and (best is None or frac > best[1]):
                best = (sd["id"], frac)
        fdta["spatial_best_sketch"] = best
        if best:
            output.print_md("- Form {}: highest spatial BBox-overlap fraction = {:.1%} with Sketch {} "
                             "(HEURISTIC ONLY).".format(fdta["id"], best[1], best[0]))
        else:
            output.print_md("- Form {}: no spatial overlap computable against any Sketch (HEURISTIC ONLY).".format(
                fdta["id"]))

    # ==============================================================
    # === DIMENSIONS -- direct References attribute, not GetDependentElements ===
    # ==============================================================
    output.print_md("\n---\n### Dimensions -- direct .References attribute (NOT GetDependentElements)")

    dims, dims_err = safe_call(lambda: list(DB.FilteredElementCollector(work_doc).OfClass(DB.Dimension)))
    dims = dims or []
    form_dimension_hits = {fdta["id"]: [] for fdta in form_data}
    sketch_dimension_hits = {sd["id"]: [] for sd in sketch_data}
    point_dimension_hits = {cp["id_str"]: [] for cp in confirmed_points}

    if dims_err:
        output.print_md("Dimension collection FAILED: {}".format(dims_err))
    else:
        output.print_md("{} Dimension element(s) found. Cross-referencing against confirmed Point/Sketch/Form "
                         "ElementIds (direct .References attribute only).".format(len(dims)))
        sketch_ids = set(sd["id"] for sd in sketch_data)
        form_ids = set(fdta["id"] for fdta in form_data)
        for d in dims:
            d_id = fmt_eid(d.Id)
            refs, refs_err = safe_call(lambda dd=d: list(dd.References))
            if refs_err or not refs:
                continue
            ref_ids = []
            for r in refs:
                try:
                    ref_ids.append(fmt_eid(r.ElementId))
                except Exception:
                    continue
            for rid in ref_ids:
                if rid in confirmed_point_ids_str:
                    point_dimension_hits[rid].append(d_id)
                if rid in sketch_ids:
                    sketch_dimension_hits[rid].append(d_id)
                if rid in form_ids:
                    form_dimension_hits[rid].append(d_id)

        any_hits = False
        for cp in confirmed_points:
            hits = point_dimension_hits[cp["id_str"]]
            if hits:
                any_hits = True
                output.print_md("- Point {} referenced by Dimension(s): {}".format(cp["id_str"], ", ".join(hits)))
        for sd in sketch_data:
            hits = sketch_dimension_hits[sd["id"]]
            if hits:
                any_hits = True
                output.print_md("- Sketch {} referenced by Dimension(s): {}".format(sd["id"], ", ".join(hits)))
        for fdta in form_data:
            hits = form_dimension_hits[fdta["id"]]
            if hits:
                any_hits = True
                output.print_md("- Form {} referenced by Dimension(s): {}".format(fdta["id"], ", ".join(hits)))
        if not any_hits:
            output.print_md("No Dimension directly references any confirmed Point/Sketch/Form ElementId "
                             "(Dimension.References attribute).")
        verified_evidence.append("{} total Dimension(s) found; direct .References cross-check against "
                                  "confirmed Point/Sketch/Form IDs performed (see detail above)".format(len(dims)))

    # ==============================================================
    # === COMPARISON BETWEEN FORMS ===
    # ==============================================================
    output.print_md("\n---\n### === COMPARISON BETWEEN FORMS ===")
    output.print_md("Setiap baris di bawah HANYA berisi evidence yang benar-benar ditemukan di atas. "
                     "'?' TIDAK PERNAH diisi tebakan -- selalu UNKNOWN kalau tidak ada evidence.")

    for fdta in form_data:
        f_id = fdta["id"]
        output.print_md("\n**Form {} ({})**".format(f_id, fdta["runtime_type"]))
        output.print_md("A. Source profile/sketch (reflection-confirmed direct link) = {}".format(
            "UNKNOWN (no reflection-discovered property on {} links directly to a Sketch on this runtime)".format(
                fdta["runtime_type"]) if not fdta["member_dump"] else
            "see reflection-relevant members above (no dedicated Sketch-typed property found by name)"))
        output.print_md("   Spatial correlation (HEURISTIC ONLY, not API-confirmed) = {}".format(
            "Sketch {} ({:.1%} BBox overlap)".format(*fdta["spatial_best_sketch"])
            if fdta["spatial_best_sketch"] else "none computable"))
        best_sketch_id = fdta["spatial_best_sketch"][0] if fdta["spatial_best_sketch"] else None
        best_sketch = next((sd for sd in sketch_data if sd["id"] == best_sketch_id), None)
        output.print_md("B. References used by that (spatially-closest, HEURISTIC) Sketch's profile curves = "
                         "{}".format(
                             ", ".join(c["ref_id"] for c in best_sketch["profile_curves"] if c["ref_id"])
                             if best_sketch and any(c["ref_id"] for c in best_sketch["profile_curves"])
                             else "UNKNOWN / none with a readable Reference"))
        output.print_md("C. Adaptive point references (direct Curve.Reference.ElementId match against the {} "
                         "confirmed Adaptive Points) = {}".format(
                             len(confirmed_points),
                             ", ".join(best_sketch["matched_point_ids"]) if best_sketch and best_sketch["matched_point_ids"]
                             else "NONE FOUND (via spatially-closest Sketch, if any)"))
        output.print_md("D. Dimension references directly on this Form = {}".format(
            ", ".join(form_dimension_hits.get(f_id, [])) or "NONE"))
        if best_sketch_id:
            output.print_md("   Dimension references on spatially-closest Sketch {} = {}".format(
                best_sketch_id, ", ".join(sketch_dimension_hits.get(best_sketch_id, [])) or "NONE"))
        output.print_md("E. Geometry construction type (GetType().Name) = **{}**".format(fdta["runtime_type"]))
        output.print_md("F. Dependency evidence to Adaptive Points (via direct attribute chain in THIS "
                         "diagnostic only, NOT GetDependentElements) = {}".format(
                             "YES (direct Curve.Reference match, see C)" if (best_sketch and best_sketch["matched_point_ids"])
                             else "NO DIRECT-ATTRIBUTE EVIDENCE FOUND (does not contradict or confirm last "
                                  "session's GetDependentElements()-based finding -- different evidence source)"))
    output.print_md("\nG. Perbandingan antar Form: lihat kolom F di atas per Form -- Form manapun yang "
                     "berbeda hasilnya (YES vs NO DIRECT-ATTRIBUTE EVIDENCE) adalah evidence-backed titik "
                     "perbedaan; interpretasi PENYEBAB perbedaan tersebut ada di bagian HYPOTHESES di bawah, "
                     "bukan di sini.")

    # ==============================================================
    # === VERIFIED API EVIDENCE (final compiled list) ===
    # ==============================================================
    output.print_md("\n---\n### === VERIFIED API EVIDENCE (compiled) ===")
    for v in verified_evidence:
        output.print_md("- {}".format(v))
    output.print_md("- Form count = {}, Sketch count = {}, Confirmed Adaptive Point count = {}, "
                     "Dimension count = {}".format(len(form_data), len(sketch_data), len(confirmed_points), len(dims)))

    # ==============================================================
    # === UNKNOWN / API LIMITATION ===
    # ==============================================================
    output.print_md("\n### === UNKNOWN / API LIMITATION ===")
    for u in unknown_items:
        output.print_md("- {}".format(u))
    output.print_md("- Form<->Sketch direct API link: TIDAK ditemukan property/method reflection pada "
                     "GenericForm/FreeFormElement CLR type di runtime ini yang secara eksplisit menghubungkan "
                     "ke Sketch tertentu -- kemungkinan linkage ini hanya terekspos lewat dependency graph "
                     "(GetDependentElements(), SENGAJA tidak dipakai di sini per instruksi sesi ini) atau "
                     "tidak terekspos publik sama sekali.")
    output.print_md("- Spatial BBox-overlap correlation adalah HEURISTIC murni -- TIDAK membuktikan hubungan "
                     "konstruksi API apa pun, hanya indikasi kedekatan geometris.")
    output.print_md("- Orientation-specific dependency (terpisah dari position/existence): masih TIDAK "
                     "TERSEDIA lewat API publik apa pun yang dipakai di sini atau di sesi sebelumnya.")

    # ==============================================================
    # === HYPOTHESES ===
    # ==============================================================
    output.print_md("\n### === HYPOTHESES ===")
    output.print_md("Semua poin di bawah BELUM terbukti oleh evidence di atas -- memerlukan konfirmasi "
                     "visual langsung di Family Editor UI (mis. via 'Select by ID').")
    yes_forms = [fdta["id"] for fdta in form_data
                 if next((sd for sd in sketch_data if fdta["spatial_best_sketch"] and sd["id"] == fdta["spatial_best_sketch"][0]), None)
                 and next((sd for sd in sketch_data if fdta["spatial_best_sketch"] and sd["id"] == fdta["spatial_best_sketch"][0]), {}).get("matched_point_ids")]
    no_forms = [fdta["id"] for fdta in form_data if fdta["id"] not in yes_forms]
    if yes_forms and no_forms:
        output.print_md("- Form {} (direct-attribute evidence ditemukan) vs Form {} (tidak) MUNGKIN "
                         "menunjukkan dua construction mechanism berbeda di family ini -- konsisten dengan "
                         "temuan sesi lalu bahwa Form 567552 unik. BELUM DIBUKTIKAN bahwa perbedaan ini "
                         "PENYEBAB rigid-rotation gagal; hanya korelasi construction-chain.".format(
                             ", ".join(yes_forms), ", ".join(no_forms)))
    output.print_md("- Kalau Form<->Sketch tidak terhubung lewat property publik apa pun (lihat UNKNOWN), "
                     "kemungkinan Form tersebut dibangun sebagai FreeFormElement dari solid langsung (bukan "
                     "sketch-driven profile) -- HYPOTHESIS, perlu klik Form tersebut di Family Editor dan "
                     "cek apakah opsi 'Edit Sketch' tersedia sama sekali.")
    output.print_md("- Dimension yang overlap dengan Sketch/Form tertentu (lihat detail Dimensions di atas) "
                     "mungkin adalah mekanisme constraint yang menahan sebagian geometry pada posisi "
                     "tetap/independen dari Adaptive Point -- HYPOTHESIS, perlu verifikasi visual constraint "
                     "tersebut di Family Editor.")

finally:
    if family_doc_opened_here and work_doc is not None:
        try:
            work_doc.Close(False)
            output.print_md("\n---\n*Family document ditutup TANPA disimpan (Close(False)).*")
        except Exception as ex:
            output.print_md("\n---\n*PERINGATAN: gagal menutup family document: {}.*".format(ex))

output.print_md("\n---\nSTOP. Read-only reflection + direct attribute access only -- TIDAK ADA "
                 "GetDependentElements() dipanggil di tool ini. Tidak ada family/geometry/parameter yang "
                 "dibuat, dihapus, atau diubah. Tidak ada Transaction dibuka. Tidak ada PASS/FAIL, tidak ada "
                 "root-cause final -- lihat pemisahan VERIFIED API EVIDENCE vs UNKNOWN vs HYPOTHESES di atas. "
                 "Jangan mengubah rotation implementation berdasarkan hasil ini.")

```

## 10. IMPORTANT LIMITATION

The four locked source files and the two older diagnostic source files are NOT reproduced in full in this dossier. Their exact SHA-256 hashes and package paths are given above. Therefore Claude can use this dossier for context and for auditing the latest diagnostic source, but cannot honestly claim a complete source-level audit of every package file unless their source is also pasted or otherwise made available. Do not pretend otherwise.

END OF DOSSIER
