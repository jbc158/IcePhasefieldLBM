########################################################################
# MechSys - Open Library for Mechanical Systems                        #
# Copyright (C) 2010 Sergio Galindo                                    #
#                                                                      #
# This program is free software: you can redistribute it and/or modify #
# it under the terms of the GNU General Public License as published by #
# the Free Software Foundation, either version 3 of the License, or    #
# any later version.                                                   #
#                                                                      #
# This program is distributed in the hope that it will be useful,      #
# but WITHOUT ANY WARRANTY; without even the implied warranty of       #
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the         #
# GNU General Public License for more details.                         #
#                                                                      #
# You should have received a copy of the GNU General Public License    #
# along with this program. If not, see <http://www.gnu.org/licenses/>  #
########################################################################


PROJECT                (MECHSYSSANDBOX)
cmake_minimum_required(VERSION 3.18)
INCLUDE(${MECHSYSSANDBOX_SOURCE_DIR}/UseMECHSYS.cmake)
SET(CUDAPROGS
    tclbm07


)



FOREACH(var ${CUDAPROGS})
    ADD_EXECUTABLE        (${var} "${var}.cu")
    TARGET_LINK_LIBRARIES (${var} ${CUDA_LIBRARIES})
    TARGET_LINK_LIBRARIES (${var} ${LIBS})
    SET_TARGET_PROPERTIES (${var} PROPERTIES COMPILE_FLAGS "${FLAGS} -DUSE_CUDA" LINK_FLAGS "${LFLAGS}")
  #  SET_TARGET_PROPERTIES (${var} PROPERTIES COMPILE_FLAGS "${FLAGS} -DUSE_CUDA -arch=sm_72" LINK_FLAGS "${LFLAGS}")
    SET_TARGET_PROPERTIES (${var} PROPERTIES CUDA_ARCHITECTURES "native")
    include_directories(/home/jibeichen/mechsys)
ENDFOREACH(var)
