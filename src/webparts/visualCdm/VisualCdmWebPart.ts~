import { Version } from '@microsoft/sp-core-library';
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField
} from '@microsoft/sp-webpart-base';
import { escape } from '@microsoft/sp-lodash-subset';

import styles from './VisualCdmWebPart.module.scss';
import * as strings from 'VisualCdmWebPartStrings';

export interface IVisualCdmWebPartProps {
  description: string;
}

class Entity {
	public name: string;
	public logic_name: string;
	public attributes: string[];
	public lookups: [string, string][];
	constructor(in_name: string, in_logic_name: string, in_attributes: string[], in_lookups: [string, string][]) 
	{ 
		this.name = in_name;  
		this.logic_name = in_logic_name;  
		this.attributes = in_attributes;  
		this.lookups = in_lookups;  
	}
}

export default class VisualCdmWebPart extends BaseClientSideWebPart<IVisualCdmWebPartProps> {

  public render(): void {

	var css = '.entityDOM:hover + .attributesDOM { display: inline-block; }';
	var style = document.createElement('style');

	if (style.style != null) {
	    style.style.cssText = css;
	} else {
	    style.appendChild(document.createTextNode(css));
	}

	document.getElementsByTagName('head')[0].appendChild(style);

	
    this.domElement.innerHTML = `
    	<canvas id="myCanvas" width="100%" height="100%" style="position: absolute; z-index: -1;">
	</canvas>
	<div class="${styles.header}" >
		This is the CDM-Model!
	</div>
	<div class="mainbody">
	</div>
      `;

      var entities: Entity[] = [];
      entities.push(
      		new Entity("Test", "new_test", ["one", "two", "three"], [["lookup_one", "new_prueba"],["lookup_two", "new_tesuto"]]),
		new Entity("Prueba", "new_prueba", ["uno", "dos", "tres"], [["buscar", "new_test"]]),	
		new Entity("Tesuto", "new_tesuto", ["ichi", "ni", "san"], [["miageru", "new_prueba"]])	
	);
	
	let main_body = document.getElementsByClassName("mainbody")[0];

	entities.forEach((item, index) => {
		var x = index * 160 + 20;
		var y = 20;
		var text_x = index * 160 + 50;
		var text_y = 50;
	
		main_body.innerHTML +=`
			<div class="${styles.entityDOM}" tag="${item.logic_name}"> 
				<div class="title">
					${item.name}
				</div>
			</div>
			<div class="${styles.attributesDOM}"> 
			</div>
		`;

		console.log(main_body);

		let attr = main_body.children[2 * (index + 1) - 1];
		item.attributes.forEach((attr_obj, attr_index) => {
			attr.innerHTML +=`
				<div class="attrLine">
					${attr_obj}
				</div>
			`;
			console.log(attr_index);
		});

	
	});
  }

  protected get dataVersion(): Version {
    return Version.parse('1.0');
  }

  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }
}
