# 

**ONTOLOGY FOR MEDIA CREATION \
PART 3A: CAMERA METADATA \
**VERSION 2.6


Contents


[1	Introduction	1](#1introduction1)
[1.1	Scope	2](#11scope2)
[1.2	Static and Dynamic Metadata	3](#12staticanddynamicmetadata3)
[1.3	Terms	3](#13terms3)
[1.4	Notational Conventions	5](#14notationalconventions5)
[2	Concepts	6](#2concepts6)
[2.1	Camera Metadata	6](#21camerametadata6)
[2.2	Lens Metadata	9](#22lensmetadata9)
[2.3	Recorder Metadata	11](#23recordermetadata11)
[3	Interaction with Other Parts of the Ontology	12](#3interactionwithotherpartsoftheontology12)
[3.1	Creative work	12](#31creativework12)
[3.2	Slate-related	12](#32slaterelated12)
[3.3	Location	13](#33location13)
[3.4	Participant	13](#34participant13)
[Appendix A	Revisions From v1.0	14](#appendixarevisionsfromv1014)
[A.1	Camera Metadata Revisions From v1.0	14](#a1camerametadatarevisionsfromv1014)
[A.2	Lens Metadata Revisions From v1.0	15](#a2lensmetadatarevisionsfromv1015)
[](#)
? 2021-2024 Motion Picture Laboratories, Inc.

This document is intended to guide companies in developing or implementing products, solutions, or services for the future of media creation. Motion Picture Laboratories, Inc. makes no effort to obligate any market participant to adhere to the recommendations in this document. Whether to adopt these recommendations in whole or in part is left to the discretion of individual market participants, using independent business judgment. Each MovieLabs member company shall decide independently the extent to which it will utilize, or require adherence to, these recommendations. All questions on member company adoption or implementation must be directed separately to each member company.


# Introduction

Picture and sound are not the only valuable data captured on a set. Metadata that tells how the picture and sound were captured is equally important and is used to help the interpretation of that data downstream of the set.  Camera Metadata is a type of Digital Asset.

For image data, the camera metadata describes, among other things, the shooting configuration of the camera. For example, whether the camera was set to record log or linear color. This is necessary for the correct interpretation of the data. If log curve images are interpreted as linear color, the result is a very ?flat? image. Correctly interpreting log color requires knowledge of the log curve[^1] that was used in the camera when the image was recorded.

![A bee on a leaf

Description automatically generated](/images/d1q-bee-leaf-description-automatically-generated.jpeg)

*Figure 1-1 Camera metadata is used to determine the LUT*[^2] *to apply to a log image*

Historically, much of the useful metadata about the camera configuration has been passed on in the notes from the camera operator. However, cameras in use today record metadata, including their settings. In the case of the image above, the camera metadata indicated it was set to log and the version of the log curve, information that was used to ?develop? the image.

Camera metadata often contains information about other parts of the capturing system. Some lenses are equipped with a means for the camera to read the settings such as aperture and focus distance. Metadata from the recorder is also important as are external inputs such as timecode.

![](/images/Rec_Image_2.png)

*Figure 1-2. Example of camera metadata captured by a DSLR*[^3] 
Figure 1-1 shows the metadata recorded by a Nikon DSLR. The camera model, serial number and lens are recorded along with metadata specific to that shot.

This document provides some definitions of common terms and classes to represent metadata from the camera system. It also describes how some other components of the Ontology can be used to provide input to the camera and how metadata from the camera system is used by other components of the Ontology.

## Scope

This document defines a set of camera metadata that is required in downstream processes including dailies and finishing, as well as VFX and Virtual Production. Other groups, such as SMPTE's Rapid Industry Solutions program for On Set Virtual Production (RIS OSVP), are creating standards for specific application areas that may be more detailed than this document.

It is not a definitive list. Some of the metadata created by the cameras is either specific to the camera model or expressed in terms that are specific to the camera model.  Color is an example of this. This document defines metadata terms for tint, white balance, saturation, and slope. However, ARRI cameras and RED cameras, for example, both have a richer set of metadata available for color, but the expression of the color parameters is specific to each camera maker.  This document does not include camera metadata used only in broadcast environment.

## Static and Dynamic Metadata

The metadata described in this document is primarily static, meaning it is time invariant between the start of recording and the end of recording. However, some metadata will change and will be recorded as such in the systems that are recording the metadata.

Obviously, each frame has a different Timecode, but other parameters may also change, for example, the Focal Length of a zoom lens and the Focus Position.

## Terms

These definitions are informative, and the ones below are normative.

| Term | Terse Definition | Notes |
|---|---|---|
| Camera | Motion picture camera | Digital unless otherwise noted as a film camera |
| LUT | Look up table | A look up table is an array, either two or three dimensional, that changes the way an image looks. For example, a LUT can be used to transform an image from one color space to another |
| ISO | The rating of the sensitivity of film or a camera sensor to light.  | The higher the ISO value, the more sensitive the film or camera imager is to light. Digital cinema cameras are often rated at 800.

?ISO? is a reference to the standards body that codified the scale. |
| EI | Exposure index | Where ISO is the rating of the film or sensor, EI is the rating at which the exposure was made.  For example, if we have a camera rated at 800 ISO and we are shooting in subdued light, we might choose to expose the image as though the imager was 1250 ISO. The EI is then used when the image is ?developed? to correct for the difference. |
| Shutter angle | A measure of the exposure time of an image relative to the frame rate. 0 < shutter angle ? 360 | Film cinema cameras use a rotating mechanical shutter that is a disc with a sector cut out and rotated one turn per frame. When the cut out passes over the film, the film is exposed to light. The most common shutter angle is 180 degrees which exposes the film for 50% of the time. If the frame rate is 24 fps, a 180-degree shutter angle would mean the exposure is 1/48th sec. This measurement is used with digital cameras although, with one exception, digital cameras have electronic shutters. |
| Timecode | A linear sequence of numeric codes generated at a regular interview and usually recorded in the format hour:minute:second:frame |  |
| FDL | Framing Decision List | The American Society of Cinematographers? FDL is a set of instructions for how to view content in any application. The ASC FDL provides a mechanism to document framing decisions through all phases of a production's life cycle, from pre-visualization through post-production. |
| Mag | Magazine | Originally, the detachable part of a film camera that held the film. With digital cameras, it means the container that holds the recording media when it is inserted into the camera or the recorder. |
| f-stop or f-number | The size of the lens aperture. | Ratio of the focal length to the diameter of the aperture. The smaller the f-stop, the larger the aperture.  |
| T-stop | The f-stop adjusted to account for light transmission efficiency | The T-stop is the f-stop corrected by a manufacturer for actual light transmission of all the lens elements, rather than the nominal aperture opening size.  |
| FPS | Frames per second | The frequency at which consecutive images (frames) are recorded or played back. |
| Frame rate | Synonymous with FPS |  |
| Lens | A device containing a series of curved glass elements used to focus light on the camera imager or film. |  |
| Recorder | A device to record to media the images captured by the camera. | The media is, for example, a solid-state disk (SSD)
 or CFast media. May be integrated into the camera. |

## Notational Conventions

*In documents generally:*

- The definition of a term included in the Dictionary is in bold, followed by the definition, e.g., **Creative Work:** A uniquely identified production.

- When a defined term is used in the text of a document, it is capitalized, for example in ?The Production Scene is usually derived from a numbered scene in the Script,? Production Scene and Script are defined in the Ontology. (Note, a word that is part of defined term may sometimes be capitalized by itself as a shorthand, e.g., ?Scene? may be used to indicate ?Narrative or Production Scene.?)

- References to other Ontology Documents are in ***bold italic***, e.g., ***Part 3: Assets ***or*** Part 3A: Camera Metadata.***

*For Sample Attributes in the concept documents:*

- If a data field or attribute is formally defined in this ontology or a connected ontology, it is italicized, e.g., *Setup *as an attribute* *refers to a defined concept.

- Attribute [?] indicates an attribute can appear more than once, e.g., *Identifier* [?]

- ?Thing means that an attribute is expressed as a relationship to a Thing, e.g., ?*Script*

- A combination of the two indicates that the concept can have relationships to a set of things, e.g., ?Components [?]

- Many elements of the Ontology have a Context element. (See **Part 2: Context**.) Relationships declared in the Context are implied to have the item to which the Context is attached as their starting point. For example, Narrative Location?Context?Narrative Scene

For clarity, contextual relationships that are especially important to the concept being defined are given in the sample attributes tables as C?target or C?target [?] as appropriate, for example Narrative Location?Narrative Scene

Some implementations (e.g. RDF) place these relationships directly on the class as well as allowing them in Context, and others (e.g. JSON) place all relationship in a Context.

# Concepts

A digital camera is a complex piece of equipment, and has multiple components: the Lens, the Camera, and either a Recorder and Mag or just a Mag. The Lens and Camera have device-specific information (make, model, etc.) and information about a particular capture. The Recorder has device-specific information and an identifier for any removable storage media (the Mag).

All of the classes have fields for both structured and unstructured representations of data not covered by the standard attributes.

The camera metadata includes a link to an FDL.  Some camera and lens metadata attributes may also appear in the FDL however since an FDL may not be present, this duplication is unavoidable. Precedence is a matter for the user.

Camera, Lens, and Recorder Metadata are all Asset Functional Classes. Assets that use them will generally have Asset Structural Characteristics that are some form of digital data (See ***Part 3: Assets***), which represents the file or other kind of storage that holds the original information generated by the device.

## Camera Metadata

**Camera Metadata:** Capture-specific details and information about the Camera itself. 

*Sample Attributes for Camera Metadata*

| Attribute | Description |
|---|---|
| Identifier [?] | One or more identifiers for the Camera Metadata. At least one of these should be resolvable within the production environment. |
| Name |  |
| Description |  |
| Attributes | See below. The Attributes are listed separately for formatting reasons; they are all individual fields, not an Array. |
| Custom Data | Anything that is application or workflow dependent that can?t be otherwise expressed in the Ontology or needs to be present in a particular format. |
| ? Context [?] | Context related to this Asset Functional Characteristic  |
| C->Slate | Camera metadata is usually associated with a particular capture, and hence with a Slate. |
| C->Camera | The Camera that generated this metadata; see Part 8: Infrastructure. |

| Term | Definition |
|---|---|
| Capture Rate | The number of individual images captured per second |
| Playback Rate | The number of individual images per second of the intended playback speed.  |
| Timecode | Timecode for each frame |
| Timecode Start | Timecode when recording started |
| Timecode End | Timecode when recorded stopped |
| Shutter Angle | A measure of the exposure time of an image relative to the frame rate. 0 < shutter angle ? 360 |
| ISO Speed | Arithmetic ISO scale as defined in ISO 12232 |
| Exposure Index | Exposure index is the ISO rating used to determine exposure when the recording was made.  |
| Reel Name | A name assigned to a sequence of recorded images |
| Camera Make | The manufacturer or vendor of the camera |
| Camera Model | The manufacturer's name for the camera model. For example, the name of the camera family followed by the name of the variant. |
| Camera UID | An alphanumeric code that uniquely identifies the camera among all cameras from all vendors |
| Camera Serial Number | An alphanumeric code assigned by the manufacturer to a camera |
| Camera Firmware Version | An alphanumeric code that identifies the firmware installed in the camera at the time of recording |
| Camera Label | Human readable ID assigned to each production camera. |
| Frame Width | The height of the intended image in pixels. This may or may not be the height of the recorded image or the sensor |
| Frame Height | The width of the intended image in pixels. This may or may not be the width of the recorded image or the sensor |
| FDL Link | Unique identifier of the FDL used by the camera |
| Active Sensor Physical Dimensions | Height and width of the active area of the camera sensor |
| Pixel Aspect Ratio | Describes how the pixels are to be interpreted to correctly display the image. |
| Flip - X | The flip-X factor indicates whether the image is flipped horizontally. |
| Flip - Y | The flip-Y factor indicates whether the image is flipped vertically. |
| LUT UID | An alphanumeric code that uniquely identifies the LUT loaded into the camera and applied to the monitor output during shooting.  |
| Tint | Defines the R/B white points against the green channel. |
| White Balance | The color temperature of white expressed in degrees Kelvin |
| Tilt | The angle of a camera off its pitch axis, measured in degrees when the camera is level |
| Roll (Dutch) | The angle of the camera off of the roll axis, measured in degrees when the camera is level |
| Camera Roll | Identifier for a group of events captured together on the same camera and recording media. |
| Circle Take | Indicating whether a recorded sequence of images is considered a candidate for use. |

*Notes:*

Structured and Unstructured Metadata have been removed since they are covered by Custom Data in the Asset.

## Lens Metadata

**Lens Metadata**: Capture-specific details and information about the Lens itself.

*Sample Attributes for Lens Metadata*

| Attribute | Description |
|---|---|
| Identifier [?] | One or more identifiers for the Lens Metadata. At least one of these should be resolvable within the production environment. |
| Name |  |
| Description |  |
| Attributes | See below. The Attributes are listed separately for formatting reasons; they are all individual fields, not an Array. |
| Custom Data | Data or metadata for a particular Functional Class. |
| ? Context [?] | Anything that is application or workflow dependent that can?t be otherwise expressed in the Ontology or needs to be present in a particular format. |
| C->Camera | The Camera associated with this Lens when the Lens Metadata was generated, if relevant; see Part 8: Infrastructure. |
| C->Lens | The Lens that generated this metadata; see Part 8: Infrastructure. |

| Term | Definition |
|---|---|
| T-Stop | The linear T-number of the lens, equal to the f-number of the lens divided by the square root of the transmittance of the lens |
| f-Stop | The linear f-number of the lens, equal to the focal length divided by the diameter of the entrance pupil |
| Entrance Pupil Position | Entrance pupil position of the lens |
| Focus Position | Focus distance/position of the lens |
| Focal Length | The actual focal length of the lens, in millimeters, when the image was captured. With a zoom lens this may be change frame by frame. |
| Lens Make | The lens manufacturer or vendor |
| Lens Model | The lens model identifier assigned by the lens manufacturer or vendor |
| Anamorphic Squeeze | Nominal ratio of height to width of the image of an axis-aligned square captured by the camera sensor |
| Lens Serial Number | A number unique to each lens from the same manufacturer or vendor and of the same model |
| Lens Firmware Version | Version identifier for the firmware of the lens |

*Notes:*

Structured and Unstructured Metadata have been removed since they are covered by Custom Data in the Asset.

## Recorder Metadata

**Recorder Metadata:** Information about a Recorder and the recording media.

*Sample Attributes for Recorder Metadata*

| Attribute | Description |
|---|---|
| Identifier [?] | One or more identifiers for the Recorder Metadata. At least one of these should be resolvable within the production environment. |
| Name |  |
| Description |  |
| Attributes | See below. The Attributes are listed separately for formatting reasons; they are all individual fields, not an Array. |
| Custom Data | Data or metadata for a particular Functional Class. |
| ? Context [?] | Anything that is application or workflow dependent that can?t be otherwise expressed in the Ontology or needs to be present in a particular format. |
| C->Camera | The Camera associated with this Lens when the Lens Metadata was generated, if relevant. |
| C->Recorder | The Recorder that generated this metadata; see Part 8: Infrastructure. |

*Sample Attributes (no change from v1.0)*

| Name | Definition |
|---|---|
| Recorder Firmware Version | An alphanumeric code that identifies the firmware installed in the recorder at the time of recording |
| Recorder Make | The recorder manufacturer or vendor |
| Recorder Model | The recorder model identifier assigned by the lens manufacturer or vendor |
| Recorder Serial Number | A number unique to each recorder from the same manufacturer or vendor and of the same model |
| Storage Media UID | An alphanumeric code that uniquely identifies the storage media (i.e., mag) the footage was recorded on to. |

*Notes:*

Structured and Unstructured Metadata have been removed since they are covered by Custom Data in the Asset.

# Interaction with Other Parts of the Ontology

Some of the data recorded by the Camera system is equivalent to information defined elsewhere in the Ontology. The flow of information goes in both directions. For instance, information about the Creative Work, such as its Director and Title, can be entered into many cameras. In the other direction, some of the information provided by the Camera is used in the Slate.

## Creative work

These are taken from the Creative Work being filmed.

| Name | Use |
|---|---|
| Title | The Title of the Creative Work can be input into a Camera. This can be a code name or in the case television a series and episode number. |

## Slate-related

The following fields of Slate are often provided in the Camera Metadata.

| Name | Definition |
|---|---|
| Slate UID | An alphanumeric code that uniquely identifies a single clip by combining the Scene Descriptor, Setup, and Take. Provided by some Cameras. |
| Scene Number | The number of the scene. Can be provided by some cameras.  |
| Shoot Date | The date the footage was captured |
| Camera Unit | A group of Participants responsible for shooting some element of a Scene, e.g., Main Unit or Second Unit. |

Some components of the Slate UID are provided by some cameras.

| Name | Definition |
|---|---|

| Scene Descriptor | The Scene Descriptor of the Production Scene being shot. |
|---|---|
| Setup | A setup is the unique camera configuration that encompasses a camera's geo-location, positioning, lens, or other camera settings. |
| Take | The events captured from the time the camera is ?rolling? to the time it is stopped. A director may require multiple takes of a Production Scene with a particular setup. |

## Location

Production Location is found in the Context Ontology.

| Name | Definition |
|---|---|
| Production Location | A real place that is used to depict the narrative location or used for creating the production. Can be provided by some Cameras. |

## Participant

These are all defined in the Participants Ontology and can be entered on some Cameras.

| Name | Definition |
|---|---|
| Director | The Camera Unit's director |
| Cinematographer | The Camera Unit's cinematographer |
| Camera Operator | The operator of the camera that recorded the footage |

1. Revisions From v1.0

In addition to updating this document as part of the MovieLabs Ontology for Media Creation, the following changes were made from v1.0.

1. Alignment with names and definitions used in SMPTE *RIS OSVP Camera and Lens Metadata Parameters for VFX*.

2. Removal of mappings to metadata definitions for three cameras from Red, ARRI and Sony. It was too small a set of camera makers and models; in general, it is not feasible to keep track of vendor?s metadata definitions.

3. Removal of mappings to *VES 1.1* and *SMPTE 2650-4* as additional standards are emerging. The mapping to SMPTE *RIS OSVP Camera and Lens Metadata Parameters for VFX* is inherent in the changes made in this version. 

Camera Metadata Revisions From v1.0

| Term | Definition | Change from v1.0 |
|---|---|---|
| Capture Rate | The number of individual images captured per second | Renamed. Was Recording FPS. |
| Playback Rate | The number of individual images per second of the intended playback speed.  | Renamed. Was Playback FPS. |
| ISO Speed | Arithmetic ISO scale as defined in ISO 12232 | Revised Definition. |
| FDL Link | Unique identifier of the FDL used by the camera | New. |
| Active Sensor Physical Dimensions | Height and width of the active area of the camera sensor | New. |

Lens Metadata Revisions From v1.0

| Term | Definition | Change for v1.0 |
|---|---|---|
| T-Stop | The linear T-number of the lens, equal to the f-number of the lens divided by the square root of the transmittance of the lens | Renamed. Was Aperture. Definition revised. |
| f-Stop | The linear f-number of the lens, equal to the focal length divided by the diameter of the entrance pupil | New. |
| Entrance Pupil Position | Entrance pupil position of the lens | New. |
| Focus Position | Focus distance/position of the lens | Renamed. Was Focus. Definition revised. |
| Anamorphic Squeeze | Nominal ratio of height to width of the image of an axis-aligned square captured by the camera sensor | Renamed. Was Lens squeeze. Definition revised. |
| Lens Firmware Version | Version identifier for the firmware of the lens | New. |

## Notes

[^1]:  For an explanation of how log curves work, see https://www.rocketstock.com/blog/tips-for-log-color-space-compositing/  
[^2]:  Look Up Table ? see Terms section
[^3]:  With still images, the metadata is often stored in the image file. 
[^4]:  https://en.wikipedia.org/wiki/CompactFlash#CFast 