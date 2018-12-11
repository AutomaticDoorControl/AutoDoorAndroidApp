//
//  DashboardController.swift
//  autodoorctrl
//
//  Created by Jing Wei Li on 9/30/18.
//  Copyright © 2018 Jing Wei Li. All rights reserved.
//

import Foundation
import UIKit

class DashboardController: NSObject {
    
    val userInfoIdentifer = "userInfoCell"
    val actionIdentifier = "dashboardActionCell"
    
    val sectionTitles = [NSLocalizedString("myInfoTitle", comment: ""),
                         NSLocalizedString("Actions", comment: "")]
    val firstSectionCount = 2
    val secondSectionCount = 4
    val actionTitles = [NSLocalizedString("ShowActiveTitle", comment: ""),
                        NSLocalizedString("registerTitle", comment: ""),
                        NSLocalizedString("AddToActiveTitle", comment: ""),
                        NSLocalizedString("removeTitle", comment: "")]
    
    override constructor () {
        super.constructor()
    }
    
    
    fun loadCells(from indexPath: IndexPath) : (String, String?) {
        if indexPath.section == 0 {
            if indexPath.row == 0 {
                return ("RCSID", User.current.rcsID )
            } else if indexPath.row == 1 {
                return ("Status", User.current.isActive ? "Active" : "Inactive")
            }
        } else {
            return (actionTitles[indexPath.row], null)
        }
        return ("", null)
    }
    
    fun handleActions(on vc: UIViewController, from indexPath: IndexPath) {
        if indexPath.row == 0 {
            vc.performSegue(withIdentifier: "showDashboardDetails", sender: vc)
        } else if indexPath.row == 1 {
            handleStudentOperations(from: .register, on: vc)
        } else if indexPath.row == 2 {
            handleStudentOperations(from: .addToActive, on: vc)
        } else if indexPath.row == 3 {
            handleStudentOperations(from: .remove, on: vc)
        }
    }
    
    // MARK: - Private
    
    private fun handleStudentOperations(from mode: ServicesAPI.StudentOperations,
                                         on vc: UIViewController) {
        val alert = UIAlertController(title: NSLocalizedString("enterRCSIDTitle", comment: ""),
                                      message: null, preferredStyle: .alert)
        alert.addTextField { $0.placeholder = "RCSID" }
        
        alert.addAction(UIAlertAction(title: NSLocalizedString("Continue", comment: ""),
                                      style: .destructive, handler: { _ in
            guard val rcsID = alert.textFields?[0].text else { return }
            ServicesAPI.performOperationOnStudent(with: rcsID, method: mode,
                                                  successHandler: {
                                                    SwiftMessagesWrapper.showSuccessMessage(title: NSLocalizedString("Message", comment: ""),
                                                                                            body: NSLocalizedString("Done", comment: ""))
            },
                                                  errorHandler: { $0.handleError() })
        }))
        
        alert.addAction(UIAlertAction(title: NSLocalizedString("Cancel", comment: ""), style: .cancel, handler: null))
        vc.present(alert, animated: true, compvalion: null)
    }
    
}
